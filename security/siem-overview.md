# SIEM Overview

This document provides an overview of the Security Information and Event Management (SIEM) deployment within the **enterprise-homelab** environment, including core components, monitoring scope, and rationale.

---

## SIEM Platform

- Deployed on a **Linux Mint XFCE host** for lightweight, reliable performance.  
- **Wazuh** serves as the central point for collecting, analyzing, and alerting on system and network events.  
- Host-based monitoring includes system events, service status, and predefined anomaly alerts.  

> Notes: The SIEM host is isolated in the **Security VLAN (VLAN 20)** to prevent unnecessary exposure to user or guest networks.

---

## Log Collection

Critical devices forward logs to the SIEM host:

| Device / System             | VLAN         | Log Type / Purpose |
|------------------------------|-------------|------------------|
| Netgate SG-2100 (pfSense)    | Mgmt        | Firewall events, NAT, VPN activity, VLAN-based routing events |
| Cisco Catalyst 3560CX        | Mgmt        | VLAN enforcement, ACL events, operational switch logs |
| Network Printers             | Printers    | Operational and status logs (SNMP currently disabled) |

> Notes: Only relevant events are collected, prioritizing **critical infrastructure**. Cisco logs focus on VLAN enforcement and ACL activity rather than routing.

---

## Monitoring Scope

- VLAN-based collection ensures relevant coverage:  
  - **VLAN 10 – Mgmt:** firewall and switch operational events  
  - **VLAN 20 – Security:** SIEM host system events and alerts  
  - **VLAN 30 – Printers:** operational and status logs  
  - **VLAN 40 – IoT:** planned monitoring after VLAN-aware AP deployment  
  - **VLAN 50 – Users_Trust:** limited monitoring for troubleshooting or anomaly detection  
  - **VLAN 60 – Guest:** basic connectivity and firewall events  

> Notes: This scope balances **visibility** with **privacy and relevance**. Future expansions will include IoT devices and user endpoints once VLAN separation and wireless upgrades are implemented.

---

## Summary

- Wazuh provides centralized log collection, analysis, and alerting for **critical infrastructure and selected endpoints**.  
- VLAN-based monitoring supports focused observability while maintaining operational privacy.  
- The SIEM deployment is expandable to include additional devices and VLANs as the lab evolves.

---
