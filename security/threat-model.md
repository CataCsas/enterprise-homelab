# Threat Model

This document outlines potential security threats to the **enterprise-homelab** environment and the controls implemented to mitigate them. It provides a high-level overview suitable for documentation and future lab improvements.

---

## Scope

- Covers internal VLANs, critical infrastructure, and wireless endpoints.  
- Focuses on risks relevant to the lab environment, including misconfigurations, unauthorized access, and exposure to the internet.  
- Future monitoring will include internal (east-west) traffic between VLANs to detect unexpected communications.  
- VLAN enforcement is handled primarily by the Cisco switch; pfSense manages routing, NAT, and DHCP.

---

## Identified Threats and Mitigations

| Threat                        | Affected Components           | Mitigation / Notes |
|--------------------------------|-----------------------------|------------------|
| Unauthorized access            | Management VLAN, SIEM host  | VLAN segregation, strong passwords, limited administrative access; administrative endpoints only |
| Misconfigured ACLs or VLANs    | Cisco switch, pfSense       | Documented VLAN design, ACL review, testing; pfSense firewall rules validated per VLAN |
| Misconfigured routing          | pfSense                      | Centralized routing/NAT ensures consistent traffic flows; internal VLANs enforced at switch |
| Compromised IoT devices        | VLAN 40 – IoT, wireless     | VLAN isolation, limited access to sensitive VLANs, planned monitoring of east-west traffic |
| Rogue wireless endpoints       | Users_Trust VLAN, Guest VLAN | Temporary isolation; future AP VLAN mapping; ACLs control lateral movement |
| Printer compromise             | VLAN 30 – Printers          | Restricted access from non-authorized VLANs, DHCP reservations, unnecessary services disabled, network printer hardening |
| Exposure to internet threats   | Edge firewall, Guest VLAN   | pfSense firewall rules, NAT, guest VLAN isolation, segregated SSID for guests |
| SIEM host compromise           | VLAN 20 – Security          | Limited access, host monitoring, regular updates, backups, isolated VLAN |

---

## Summary

- Threats are mitigated primarily through **VLAN segmentation**, **centralized firewall enforcement**, **ACLs**, and **host monitoring**.  
- VLAN-aware wireless and additional endpoints will follow the same security principles.  
- Documentation ensures risks are visible and mitigations are repeatable, supporting a professional SOC-style lab management approach.

---
