# Logging Scope

This document defines the scope of log collection and monitoring for the **enterprise-homelab** SIEM deployment. It outlines which devices, VLANs, and services are monitored, and the rationale for their inclusion.

---

## Monitored Devices and Systems

| Device / System             | VLAN         | Log Type / Purpose |
|-----------------------------|-------------|------------------|
| Linux SIEM Notebook         | Security    | Central log aggregation, host monitoring |
| Netgate SG-2100 (pfSense)   | Mgmt        | Firewall logs, VLAN-based routing events, VPN activity |
| Cisco Catalyst 3560CX       | Mgmt        | VLAN enforcement, access control events, switch operational logs |
| Network Printers            | Printers    | Operational logs and status events (SNMP currently disabled) |

> Notes:  
> - Logs are collected centrally on the SIEM host.  
> - Devices are monitored to provide visibility into **critical network and system activity**.  
> - Cisco switch logs focus on **segmentation and ACL enforcement**, not routing.

---

## VLAN Coverage

- **VLAN 10 – Mgmt:** Management traffic, firewall and switch activity  
- **VLAN 20 – Security:** SIEM host and security-critical devices  
- **VLAN 30 – Printers:** Operational and status logging  
- **VLAN 40 – IoT:** Planned monitoring for IoT devices after VLAN-aware wireless deployment  
- **VLAN 50 – Users_Trust:** Monitoring limited to troubleshooting, anomaly detection, and DHCP leases  
- **VLAN 60 – Guest:** Basic connectivity and firewall logs; no detailed endpoint monitoring  

> Notes:  
> - VLAN selection balances **visibility** with **privacy and relevance**.  
> - IoT and Users_Trust VLAN monitoring may expand once VLAN-aware wireless and access policies are implemented.

---

## Log Types and Forwarding

- Syslog is used where supported; SNMP is currently disabled for printers.  
- Host-based logs (Linux SIEM) include system events, service monitoring, and anomaly alerts.  
- Network devices forward logs directly to the SIEM host for aggregation and alerting.  

> Notes:  
> - Log retention, rotation, and analysis policies are documented separately in the SIEM configuration.  
> - The scope prioritizes **critical infrastructure first**, then expands to other VLANs as the lab evolves.  
> - VLAN-aware monitoring ensures logs reflect **segmentation enforcement** and traffic policies.

---

## Summary

- The SIEM collects logs from **critical infrastructure and selected endpoints** to maintain situational awareness.  
- VLAN-based scope ensures relevant coverage while minimizing unnecessary logging.  
- Future expansions will include IoT and user devices after VLAN separation, VLAN-aware wireless, and access policies are fully implemented.

---
