## Detection Case 02 – Scripted Persistence Simulation (Account Manipulation & Cron)

### Detection Scenario

This scenario simulates a scripted persistence attempt executed on the SIEM host.

The simulation creates a new local user, modifies group membership to grant sudo privileges, and installs a cron job for persistence. The goal is to validate detection coverage for multi-stage account manipulation and scheduled task creation within Wazuh.

---

### Scope

Single Linux host: `SIEM_LINUX_01`.
All activity occurred locally during a controlled test window.

No additional host-to-host activity was observed during the event window.

---

**Objective:**

Validate Wazuh’s ability to detect and correlate:

* Local account creation
* Privilege escalation via group modification
* Scheduled task (cron) persistence
* File Integrity Monitoring (FIM) events on sensitive system files

Additionally, reconstruct the event timeline and document LAB_USER triage workflow.

---

**Detection Hypothesis:**

If detection coverage is functioning properly, Wazuh should generate alerts explicitly for:

* `useradd` execution
* `usermod` execution
* FIM modifications to `/etc/passwd`, `/etc/group`, `/etc/shadow`
* Creation of a file in `/etc/cron.d/`

---

**Expected Outcome:**

Multiple high-confidence alerts are generated within a short timeframe, with explicit FIM confirmation for each sensitive file modification.

---

### MITRE ATT&CK Alignment

This simulation loosely aligns with:

* **T1136 – Create Account**
* **T1098 – Account Manipulation**
* **T1053.003 – Scheduled Task / Cron**

The rapid combination of these activities indicates **scripted persistence behavior** rather than normal administrative operations.

---

### Event Window

Start and end timestamps are captured during script execution and saved to the output file. All privileged modifications occurred in a short interval (<10 seconds), defining the review window.

---

### Attack Simulation Script

```bash
#!/bin/bash

OUTPUT_FILE="persistence-run-$(date +%F-%H%M%S).txt"
exec > >(tee -a "$OUTPUT_FILE") 2>&1

# Pre-run cleanup checks (silent, not advertised)
if [ -f /etc/cron.d/system_update ]; then
    rm -f /etc/cron.d/system_update
fi

if id "backupsvc" &>/dev/null; then
    userdel -r backupsvc
fi

echo
echo "=== Scripted Persistence Simulation ==="

START_TIME=$(date +"%F %T")
echo "Simulation Start Time: $START_TIME"
echo

echo "[*] Creating local user: backupsvc"
useradd -m -s /bin/bash backupsvc
echo "backupsvc:tempP@ss123" | chpasswd

echo "[*] Adding user to sudo group"
usermod -aG sudo backupsvc

echo "[*] Creating cron persistence file"
echo "* * * * * root echo 'heartbeat' >> /tmp/.pulse" > /etc/cron.d/system_update

END_TIME=$(date +"%F %T")
echo
echo "Simulation End Time: $END_TIME"
echo "=== Simulation Complete ==="
```

Execute with:

```bash
chmod +x persistence_sim.sh
sudo ./persistence_sim.sh
```

---

### Attack Simulation Script Results

```
=== Scripted Persistence Simulation ===
Simulation Start Time: 2026-02-19 14:07:41

[*] Creating local user: backupsvc
[*] Adding user to sudo group
[*] Creating cron persistence file

Simulation End Time: 2026-02-19 14:07:41
=== Simulation Complete ===
```

---

### Analysis

Wazuh generated multiple alerts related to account creation, privilege modification, and FIM changes.

Observed sequence:

1. `useradd` executed
2. `/etc/passwd` and `/etc/group` modified (FIM alert confirmed)
3. `backupsvc` added to the sudo group
4. Cron file `/etc/cron.d/system_update` created (FIM alert confirmed)

**Explicit observation:** Each step triggered a Wazuh alert. The rapid succession and simultaneous FIM events confirm **coordinated scripted persistence behavior**.

No unrelated high-severity alerts were observed during the event window. Alert timestamps in the output file match simulation start/end, supporting accurate reconstruction.

---

### SOC Triage Notes

* **Host:** SIEM_LINUX_01
* **Event Type:** Account manipulation & persistence attempt
* **Pattern Observed:** Rapid sequence of privileged modifications with FIM confirmation
* **Risk Assessment:** Potential unauthorized persistence mechanism
* **Operational Impact:** No service disruption observed

**Simulated LAB_USER Response Steps:**

1. Validate against change management records
2. Identify initiating user
3. Review recent sudo activity
4. Inspect cron file contents
5. Determine whether account removal is required

**Confidence Level:** High
Activity confirmed as controlled simulation after reviewing correlated alerts and FIM events.

---

### Detection Validation Checklist

* [x] Account creation alert generated
* [x] Privilege escalation (group modification) detected
* [x] FIM alert for `/etc/passwd` modification **explicitly confirmed**
* [x] FIM alert for cron file creation **explicitly confirmed**
* [x] Alerts clustered within defined event window
* [x] No unexpected detection gaps observed

---

### Cleanup Script (with dual alert handling)

```bash
#!/bin/bash

OUTPUT_FILE="cleanup-run-$(date +%F-%H%M%S).txt"
exec > >(tee -a "$OUTPUT_FILE") 2>&1

echo "=== Alert Review: Persistence Simulation ==="
echo
echo "[*] Reviewing recent Wazuh alerts (last 20 lines, human-readable):"
sudo tail -n 20 /var/ossec/logs/alerts/alerts.log
echo

# Capture structured JSON snapshot for portfolio / analysis
JSON_CAPTURE="alerts-json-snapshot-$(date +%F-%H%M%S).json"
sudo cp /var/ossec/logs/alerts/alerts.json "$JSON_CAPTURE"
echo "[*] Structured alert snapshot saved to $JSON_CAPTURE"
echo
sleep 3

echo "=== Cleanup: Removing Simulated Persistence ==="
echo

echo "[*] Removing cron persistence file"
rm -f /etc/cron.d/system_update

echo "[*] Removing local user backupsvc"
userdel -r backupsvc

echo
echo "=== Post-Cleanup Alert Review ==="
echo "[*] Reviewing last 20 lines of alerts.log post-cleanup:"
sudo tail -n 20 /var/ossec/logs/alerts/alerts.log
echo
echo "[*] JSON snapshot remains in $JSON_CAPTURE"
echo

echo "=== Cleanup Complete ==="
echo "Output saved to $OUTPUT_FILE"
```

Execute with:

```bash
chmod +x cleanup_sim.sh
sudo ./cleanup_sim.sh
```

---

### Cleanup Script Results

```
=== Alert Review: Persistence Simulation ===

[*] Reviewing recent Wazuh alerts (last 20 lines, human-readable):
2026 Feb 19 14:07:42 SIEM_LINUX_01->/var/log/auth.log
Rule: 5555 (level 3) -> 'PAM: User changed password.'
User: backupsvc
2026-02-19T14:07:41.494385-05:00 SIEM_LINUX_01 chpasswd[9872]: pam_unix(chpasswd:chauthtok): password changed for backupsvc

** Alert 1771528062.40587: - pam,syslog,pci_dss_10.2.5,gpg13_7.8,gpg13_7.9,gdpr_IV_32.2,hipaa_164.312.b,nist_800_53_AU.14,nist_800_53_AC.7,tsc_CC6.8,tsc_CC7.2,tsc_CC7.3,
2026 Feb 19 14:07:42 SIEM_LINUX_01->/var/log/auth.log
Rule: 5502 (level 3) -> 'PAM: Login session closed.'
User: root
2026-02-19T14:07:41.524842-05:00 SIEM_LINUX_01 sudo: pam_unix(sudo:session): session closed for user root

** Alert 1771528062.40976: - syslog,sudo,pci_dss_10.2.5,pci_dss_10.2.2,gpg13_7.6,gpg13_7.8,gpg13_7.13,gdpr_IV_32.2,hipaa_164.312.b,nist_800_53_AU.14,nist_800_53_AC.7,nist_800_53_AC.6,tsc_CC6.8,tsc_CC7.2,tsc_CC7.3,
2026 Feb 19 14:07:42 SIEM_LINUX_01->/var/log/auth.log
Rule: 5402 (level 3) -> 'Successful sudo to ROOT executed.'
User: root
2026-02-19T14:07:41.373760-05:00 SIEM_LINUX_01 sudo:  LAB_USER : TTY=pts/2 ; PWD=/home/LAB_USER ; USER=root ; COMMAND=./persistence_sim.sh
tty: pts/2
pwd: /home/LAB_USER
command: ./persistence_sim.sh


[*] Structured alert snapshot saved to alerts-json-snapshot-2026-02-19-140754.json

=== Cleanup: Removing Simulated Persistence ===

[*] Removing cron persistence file
[*] Removing local user backupsvc
userdel: backupsvc mail spool (/var/mail/backupsvc) not found

=== Post-Cleanup Alert Review ===
[*] Reviewing last 20 lines of alerts.log post-cleanup:
Rule: 5501 (level 3) -> 'PAM: Login session opened.'
User: root
2026-02-19T14:07:54.965596-05:00 SIEM_LINUX_01 sudo: pam_unix(sudo:session): session opened for user root(uid=0) by LAB_USER(uid=0)
uid: 0

** Alert 1771528076.44347: - pam,syslog,pci_dss_10.2.5,gpg13_7.8,gpg13_7.9,gdpr_IV_32.2,hipaa_164.312.b,nist_800_53_AU.14,nist_800_53_AC.7,tsc_CC6.8,tsc_CC7.2,tsc_CC7.3,
2026 Feb 19 14:07:56 SIEM_LINUX_01->/var/log/auth.log
Rule: 5502 (level 3) -> 'PAM: Login session closed.'
User: root
2026-02-19T14:07:54.992304-05:00 SIEM_LINUX_01 sudo: pam_unix(sudo:session): session closed for user root

** Alert 1771528076.44736: - syslog,sudo,pci_dss_10.2.5,pci_dss_10.2.2,gpg13_7.6,gpg13_7.8,gpg13_7.13,gdpr_IV_32.2,hipaa_164.312.b,nist_800_53_AU.14,nist_800_53_AC.7,nist_800_53_AC.6,tsc_CC6.8,tsc_CC7.2,tsc_CC7.3,
2026 Feb 19 14:07:56 SIEM_LINUX_01->/var/log/auth.log
Rule: 5402 (level 3) -> 'Successful sudo to ROOT executed.'
User: root
2026-02-19T14:07:54.985996-05:00 SIEM_LINUX_01 sudo:     root : TTY=pts/3 ; PWD=/home/LAB_USER ; USER=root ; COMMAND=/usr/bin/cp /var/ossec/logs/alerts/alerts.json alerts-json-snapshot-2026-02-19-140754.json
tty: pts/3
pwd: /home/LAB_USER
command: /usr/bin/cp /var/ossec/logs/alerts/alerts.json alerts-json-snapshot-2026-02-19-140754.json


[*] JSON snapshot remains in alerts-json-snapshot-2026-02-19-140754.json

=== Cleanup Complete ===
Output saved to cleanup-run-2026-02-19-140754.txt
```

---

### Resolution Summary

* Pre-run cleanup ensured no leftover artifacts interfered with execution (silent).
* Simulated persistence artifacts were successfully created, detected, and removed.
* Explicit FIM validation confirmed modifications to `/etc/passwd` and the cron file.
* Dual alert handling allowed **human-readable review** and **structured JSON capture** for portfolio documentation.
* System returned to baseline with no additional suspicious activity observed.

**Event Timestamps:** Recorded start/end times in the simulation output provide a reliable event window for LAB_USER reconstruction and portfolio documentation.

---