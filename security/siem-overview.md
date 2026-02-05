# SIEM Overview

This document provides an overview of the Security Information and Event Management (SIEM) deployment within the **enterprise-homelab** environment. It describes the platform, log sources, monitoring scope, and the rationale behind a selective, infrastructure-focused approach.

---

## SIEM Platform

- Deployed on a **Linux Mint XFCE host** for lightweight and stable operation.  
- **Wazuh** is used for centralized log collection, analysis, and alerting.  
- Host-based monitoring applies only to the SIEM system itself and includes:
  - System and service events
  - Agent health and integrity
  - Predefined anomaly detection

The SIEM host is isolated in **VLAN 20 – Security** to reduce exposure and align with enterprise SOC architectures.

---

## Log Collection Sources

The SIEM ingests logs from critical infrastructure components:

| Device / System           | VLAN      | Log Type / Purpose |
|---------------------------|-----------|-------------------|
| Netgate SG-2100 (pfSense) | Mgmt      | Firewall allow/deny events, inter-VLAN policy enforcement, routing decisions |
| Cisco Catalyst 3560CX     | Mgmt      | VLAN enforcement, ACL activity, switch operational logs |
| Network Printers          | Printers  | Limited operational and status events |

**Notes:**
- Logging is **explicit and selective**, not blanket-enabled.
- Cisco switch logs focus on **segmentation and access control**, not routing.
- SNMP is currently disabled on printers; logging is minimal by design.

---

## Monitoring Scope by VLAN

- **VLAN 10 – Mgmt**  
  Firewall and switch control-plane events, administrative access activity.

- **VLAN 20 – Security**  
  SIEM host logs, agent status, and alerting activity.

- **VLAN 30 – Printers**  
  Basic availability and policy-compliance visibility.

- **VLAN 40 – IoT**  
  Defined and secured, but **not currently active**. No log sources present.

- **VLAN 50 – Users_Trust**  
  No endpoint-level monitoring. Visibility limited to:
  - Firewall enforcement events
  - DHCP activity
  - Anomalous or policy-violating traffic patterns

- **VLAN 60 – Guest**  
  Defined and secured, but **not currently active**. Once enabled, visibility will be limited to firewall enforcement only.

This scope balances **security visibility, performance, and privacy**, reflecting common enterprise SOC practices.

---

## Design Rationale

- Prioritize **infrastructure and control-plane visibility**.
- Avoid excessive endpoint logging that produces noise without actionable value.
- Ensure all monitored events clearly map to:
  - Segmentation enforcement
  - Access control decisions
  - Policy violations

Logging scope expands only when it provides measurable operational or security benefit.

---

## Summary

- Wazuh provides centralized visibility into **critical network and security infrastructure**.
- Monitoring is VLAN-aware and intentionally selective.
- User, IoT, and Guest monitoring is limited or deferred by design.
- The SIEM architecture supports future expansion without requiring redesign.

---
