# SIEM Overview

This document provides an overview of the Security Information and Event Management (SIEM) deployment within the **enterprise-homelab** environment, including core components, monitoring scope, and rationale.

---

## SIEM Platform

- Deployed on a **Linux Mint XFCE host** for lightweight, reliable performance.  
- **Wazuh** serves as the central point for collecting, analyzing, and alerting on system and network events.  
- Host-based monitoring includes system events, service status, and predefined anomaly alerts.

---

## Log Collection

Critical devices forward logs to the SIEM host:

| Device / System             | VLAN         | Log Type / Purpose |
|------------------------------|-------------|------------------|
| Netgate SG-2100 (pfSense)    | Mgmt        | Firewall events, VPN activity, network events |
| Cisco Catalyst 3560CX        | Mgmt        | VLAN traffic summaries, ACL events, system logs |
| Network Printers             | Printers    | Operational and status logs (SNMP currently disabled) |

> Notes: Only relevant events are collected, prioritizing infrastructure and security-critical devices.

---

## Monitoring Scope

- VLAN-based collection ensures relevant coverage:  
  - **VLAN 10 – Mgmt:** firewall and switch activity  
  - **VLAN 20 – Security:** SIEM host activity  
  - **VLAN 30 – Printers:** operational logs  
  - **VLAN 40 – IoT:** planned monitoring after VLAN-aware AP deployment  
  - **VLAN 50 – Users_Trust:** limited monitoring for troubleshooting or anomalies  
  - **VLAN 60 – Guest:** basic connectivity and firewall events  

---

## Summary

- Wazuh provides centralized log collection, analysis, and alerting for critical infrastructure and selected endpoints.  
- VLAN segmentation supports focused monitoring and preserves visibility.  
- The SIEM deployment is expandable to include additional devices and VLANs as the lab evolves.

---
