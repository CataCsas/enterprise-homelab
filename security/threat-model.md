# Threat Model

This document outlines potential security threats to the **enterprise-homelab** environment and the controls implemented to mitigate them. It provides a high-level overview suitable for documentation and future lab improvements.

---

## Scope

- Covers internal VLANs, critical infrastructure, and wireless endpoints.  
- Focuses on risks relevant to the lab environment, including misconfigurations, unauthorized access, and exposure to the internet.  

---

## Identified Threats and Mitigations

| Threat                        | Affected Components           | Mitigation / Notes |
|--------------------------------|-----------------------------|------------------|
| Unauthorized access            | Management VLAN, SIEM host  | VLAN segregation, strong passwords, limited administrative access |
| Misconfigured routing or ACLs  | L3 switch, firewall         | Documented SVI configuration, ACL review, and testing |
| Compromised IoT devices        | VLAN 40 – IoT, wireless    | VLAN isolation, limited access to sensitive VLANs, planned monitoring |
| Rogue wireless endpoints       | Users_Trust VLAN, Guest VLAN | VLAN segregation, temporary wireless isolation, future AP VLAN mapping |
| Printer compromise             | VLAN 30 – Printers         | Restricted access from non-authorized VLANs, DHCP reservations, unnecessary services disabled, network printer hardening |
| Exposure to internet threats   | Edge firewall, Guest VLAN   | pfSense firewall rules, NAT, guest VLAN isolation |
| SIEM host compromise           | VLAN 20 – Security          | Limited access, host monitoring, regular updates, backups |

---

## Summary

- Threats are mitigated primarily through **VLAN segmentation**, **access control**, and **centralized monitoring**.  
- Future expansions, including VLAN-aware wireless and additional devices, will follow the same security principles.  
- Documentation ensures risks are visible and controls are repeatable, supporting professional lab management.

---
