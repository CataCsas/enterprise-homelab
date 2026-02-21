## Detection Case 01 – Failed Sudo Escalation (Wazuh Rule 5404)

**Objective:**
Simulate authentication failures on VLAN_SIEM to validate SIEM ingestion and correlation.

**Expected outcome:**
Wazuh rule 5404 (level 10) triggers after three failed sudo attempts.

> Note: hostnames, usernames, and VLAN identifiers shown are intentionally placeholders used in a controlled home lab environment.

```bash
#!/bin/bash

# Timestamped output file
OUTPUT_FILE="wazuh-capture-$(date +%F-%H%M%S).txt"
exec > >(tee -a "$OUTPUT_FILE") 2>&1

echo "=== Test VLAN20-SIEM connectivity with alert ==="
echo

# Hostname
echo "Hostname:"
hostname
echo

# Detect primary interface
PRIMARY_IF=$(ip route | awk '/default/ {print $5}')
echo "Primary Network Interface:"
echo "$PRIMARY_IF"
echo
echo "Primary Interface IPv4:"
ip -brief -4 address show "$PRIMARY_IF"
echo

# Wazuh
echo "Wazuh Agent status:"
sudo /var/ossec/bin/agent_control -l
echo

# Generate alert by manually failing sudo password 3 times
echo "Manual sudo test to generate failed password attempts:"
sudo -k
echo "When prompted, enter the wrong password 3 times to trigger Wazuh rule 5404"
echo
sleep 1
sudo visudo
echo
echo "Test complete! Wait for Wazuh to ingest..."
echo
sleep 5

# Capture recent Wazuh alerts
echo "Recent Wazuh alerts (last 20 lines):"
sudo tail -n 20 /var/ossec/logs/alerts/alerts.log
echo

echo "=== End of capture ==="
echo "Output saved to $OUTPUT_FILE"
```
=== Test VLAN20-SIEM connectivity with alert ===

Hostname:
SIEM_LINUX_01

Primary Network Interface:
enp2s0

Primary Interface IPv4:
enp2s0           UP             VLAN_SIEM 

Wazuh Agent status:

Wazuh agent_control. List of available agents:
   ID: 000, Name: SIEM_LINUX_01 (server), IP: 127.0.0.1, Active/Local

List of agentless devices:


Manual sudo test to generate failed password attempts:
When prompted, enter the wrong password 3 times to trigger Wazuh rule 5404

sudo: 3 incorrect password attempts

Test complete! Wait for Wazuh to ingest...

Recent Wazuh alerts (last 20 lines):
2026-02-18T17:50:23.049105-05:00 SIEM_LINUX_01 sudo: pam_unix(sudo:session): session closed for user root

** Alert 1771455040.40621: - pam,syslog,authentication_failed,pci_dss_10.2.4,pci_dss_10.2.5,gpg13_7.8,gdpr_IV_35.7.d,gdpr_IV_32.2,hipaa_164.312.b,nist_800_53_AU.14,nist_800_53_AC.7,tsc_CC6.1,tsc_CC6.8,tsc_CC7.2,tsc_CC7.3,
2026 Feb 18 17:50:40 SIEM_LINUX_01->/var/log/auth.log
Rule: 5503 (level 5) -> 'PAM: User login failed.'
User: LAB_USER
2026-02-18T17:50:39.530220-05:00 SIEM_LINUX_01 sudo: pam_unix(sudo:auth): authentication failure; logname= uid=1000 euid=0 tty=/dev/pts/3 ruser=LAB_USER rhost=  user=LAB_USER
uid: 1000
euid: 0
tty: /dev/pts/3

** Alert 1771455052.41163: - syslog,sudo,pci_dss_10.2.4,pci_dss_10.2.5,gpg13_7.8,gdpr_IV_35.7.d,gdpr_IV_32.2,hipaa_164.312.b,nist_800_53_AU.14,nist_800_53_AC.7,tsc_CC6.1,tsc_CC6.8,tsc_CC7.2,tsc_CC7.3,
2026 Feb 18 17:50:52 SIEM_LINUX_01->/var/log/auth.log
Rule: 5404 (level 10) -> 'Three failed attempts to run sudo'
User: root
2026-02-18T17:50:50.606514-05:00 SIEM_LINUX_01 sudo:  LAB_USER : 3 incorrect password attempts ; TTY=pts/3 ; PWD=/home/LAB_USER ; USER=root ; COMMAND=/usr/sbin/visudo
tty: pts/3
pwd: /home/LAB_USER
command: /usr/sbin/visudo


=== End of capture ===
Output saved to wazuh-capture-2026-02-18-175023.txt

### Analysis

The 5503 alert confirms individual PAM authentication failures recorded in `/var/log/auth.log`.

After three consecutive failed sudo attempts, Wazuh correlates these events and triggers rule 5404 (level 10), indicating a potential privilege escalation attempt via repeated authentication failure.

This validates successful log ingestion, event parsing, and rule correlation within the SIEM environment.

### SOC Triage Notes

- Source host: LAB-USER (sanitized)
- Event type: Privileged authentication failure
- Pattern: 3 consecutive failures within short interval
- Risk Assessment: Possible brute-force or unauthorized privilege escalation attempt
- Recommended Action: Validate user intent, confirm no unauthorized access, check for repeated behavior