# Jira Service Management – IT Workflow Simulation

This document showcases a simulated ITSM workflow using **Jira Service Management** as part of my enterprise home lab. It demonstrates:

- Incident triage and investigation
- Service request handling
- Prioritization and lifecycle management
- Realistic workflow states and resolution documentation

---

## Overview – Board View

This board snapshot represents an active IT workflow with mixed incident and service request tickets across priorities.

![Jira Board Overview](./docs/assets/jira/jira-board-overview.png)

---

## Example Incident – Suspicious Login Investigation

This incident shows cross-system log analysis, user validation, and investigation steps before closure.

![Suspicious Login Detail](./docs/assets/jira/jira-suspicious-login.png)

**Key points:**

- High-priority security incident
- Verified logs and contacted user
- Confirmed legitimate access, closed as verified

---

## 🛠️ Example Service Request – Password Reset

This ticket illustrates a standard IT support service request lifecycle from start to resolution.

![Password Reset Detail](./docs/assets/jira/jira-password-reset.png)

**Key points:**

- Internal notes for identity verification
- Status transitions: Waiting → In Progress → Resolved
- Clear resolution steps and confirmation

---

## Complete Ticket Set – Written Summary

The following ticket set reflects simulated incidents and service requests created in Jira Service Management as part of the lab environment. Each ticket includes Work Type, Request Type, Summary, Components or Select a system (where applicable), Priority, and Description, along with the workflow phases Investigation / Troubleshooting and Resolution / Closure.

---

### **Ticket 1 – Failed sudo attempts (Rule 5404)**

* **Work Type:** [System] Incident
* **Request Type:** Report a system problem
* **Summary:** SIEM alert: multiple failed sudo attempts on lab-host-01
* **Priority/Urgency/Impact:** Medium / Medium / Moderate
* **Description:**
Our SIEM generated a Rule 5404 alert indicating multiple failed sudo attempts on lab-host-01. I checked with the assigned user, and they are not aware of any recent privilege changes or administrative actions. Requesting investigation to determine if this is suspicious activity or a false positive.

**Investigation / Troubleshooting:**
* Reviewed `/var/log/auth.log` for failed authentication entries.
* PAM logs confirmed 3 consecutive failed sudo attempts.
* Checked for correlated alerts (Rule 5503 or brute force patterns). No lateral movement or additional hosts involved.

**Resolution / Closure:**
* Determined activity consistent with mistyped password.
* No unauthorized access or privilege escalation occurred.
* Monitored host for additional attempts over 24 hours. Incident closed as benign user error.

---

### **Ticket 2 – Unauthorized Account Creation**

* **Work Type:** [System] Incident
* **Request Type:** Report a system problem
* **Summary:** unauthorized account creation & cron persistence on lab-host-02
* **Priority/Urgency/Impact:** Highest / High / Significant
* **Description:**
Multiple SIEM alerts were triggered on lab-host-02 related to new user creation and system file modifications. The activity was not associated with a scheduled change. Requesting investigation to determine whether this represents unauthorized persistence activity.

**Investigation / Troubleshooting:**
* Cross-checked against change management logs. Confirmed `useradd` and `usermod` entries in audit logs.
* Inspected cron file and sudo group membership. FIM detected changes to `/etc/passwd`, `/etc/group`, and `/etc/cron.d/`.
* No approved change request found.
* Determined alerts were part of controlled lab simulation.

**Resolution / Closure:**
* Removed simulated account and deleted cron persistence file.
* Verified file integrity returned to baseline.
* Documented timeline and closed the ticket.

---

### **Ticket 3 – Firewall Change – Add VLAN20 DNS/NTP Rule**

* **Work Type:** [System] Service request
* **Request Type:** No request type
* **Summary:** VLAN20 DNS/NTP firewall update
* **Components:** Office Network
* **Priority/Urgency/Impact:** Medium / Medium / Moderate
* **Description:**
Devices in VLAN20 are unable to resolve DNS or sync time via NTP. This is affecting update checks and system synchronization. Requesting firewall rule review to restore required outbound services.

**Investigation / Troubleshooting:**
* Verified affected services and potential operational impact.
* Confirmed traffic blocked at pfSense firewall. No existing allow rule for VLAN20 → DNS/NTP.
* Reviewed network segmentation to ensure security compliance.

**Resolution / Closure:**
* Implemented outbound allow rule for DNS (TCP/UDP 53) and NTP (UDP 123).
* Tested connectivity from VLAN20 host. Confirmed services operational.
* Documented change for operational record; ticket closed.

---

### **Ticket 4 – Provision Azure AD User**

* **Work Type:** [System] Service request
* **Request Type:** Request a new account
* **Summary:** provision Azure AD user (least privilege)
* **Select a system:** Active Directory
* **Priority/Urgency/Impact:** Medium / Medium / Moderate
* **Description:**
Requesting creation of a new Azure AD account for lab testing purposes. Access required: standard user permissions only. No administrative roles needed.

**Investigation / Troubleshooting:**
* Verified purpose, access scope, and least-privilege requirements.
* Confirmed no license conflicts.

**Resolution / Closure:**
* Account created.
* Assigned appropriate role.
* Verified login successful.

---

### **Ticket 5 – Password Reset**

* **Work Type:** [System] Service request
* **Request Type:** Get IT help
* **Summary:** password reset for Azure AD user
* **Priority/Urgency/Impact:** Low / Low / Minor
* **Description:**
User reports inability to log into Azure AD account due to forgotten password and requests password reset assistance.

**Investigation / Troubleshooting:**
* Verified user identity and account ownership.
* Reviewed recent login activity; no suspicious behavior detected.
* Ensured password policy compliance.

**Resolution / Closure:**
* Password reset performed.
* Temporary credentials issued.
* User confirmed successful login.

---

### **Ticket 6 – Suspicious Login Investigation**

* **Work Type:** [System] Incident
* **Request Type:** Report a system problem
* **Summary:** suspicious login from external IP
* **Priority/Urgency/Impact:** High / High / Significant
* **Description:**
VPN logs indicate a successful login from an external IP address not previously associated with the user. The geographic location appears unusual. Requesting validation of login legitimacy.

**Investigation / Troubleshooting:**
* Cross-checked VPN logs and user activity.
* Contacted user to confirm legitimate access.
* Verified MFA was successfully completed.

**Resolution / Closure:**
* User confirmed legitimate travel-related access.
* No indicators of compromise identified.
* Incident closed as verified legitimate activity.

---

### **Ticket 7 – Deploy Lab VM**

* **Work Type:** [System] Service request
* **Request Type:** No request type
* **Summary:** deploy lab VM for testing
* **Components:** Cloud Storage Services
* **Priority/Urgency/Impact:** Low / Medium / Moderate
* **Description:**
Requesting deployment of a new lab VM for security testing and network validation exercises. Standard configuration required (no external exposure). Please confirm resource availability.

**Investigation Notes:**
* Checked resource availability.
* Verified network access requirements.
* Confirmed no naming conflicts with existing lab hosts.

**Resolution / Action Taken:**
* VM deployed and configured with required services.
* Connectivity and access verified.
* Handover completed.

---

### **Ticket 8 – User Deprovision**

* **Work Type:** [System] Service request
* **Request Type:** Get IT help
* **Summary:** deprovision lab user and remove access
* **Priority/Urgency/Impact:** Lowest / High / Significant
* **Description:**
Lab user account is no longer required. Please disable account and remove associated access to ensure compliance with least privilege and lifecycle management.

**Investigation Notes:**
* Identified all group memberships.
* Reviewed active sessions.
* Confirmed no dependencies.

**Resolution / Action Taken:**
* Account disabled.
* Roles and group memberships removed.
* Access revocation verified.

---
