# Wireless Network

This document outlines the wireless network design for the **enterprise-homelab** environment, including the current temporary setup and planned upgrades.

---

## Temporary Wireless Deployment

- A **Velop mesh** provides wireless coverage temporarily.  
- All wireless endpoints, including IoT devices, are currently consolidated on **VLAN 50 – Users_Trust**.  
- IP addressing follows the VLAN DHCP scheme from the Cisco L3 switch.  
- The Velop operates in **bridge mode**, leaving routing and VLAN segmentation to the L3 switch.

> Notes:  
> - This temporary setup simplifies connectivity while maintaining basic internal control.  
> - Internal traffic continues to be routed and monitored via the L3 switch.

---

## Planned Wireless Upgrade

- **TP-Link EAP610** access points will replace the Velop mesh.  
- VLAN tagging will separate wireless traffic into:  
  - **VLAN 40 – IoT**  
  - **VLAN 50 – Users_Trust**  
  - **VLAN 60 – Guest**  
- Each SSID will map to its respective VLAN for proper segmentation.  
- DHCP and inter-VLAN routing will remain centralized on the Cisco L3 switch.  
- Future monitoring will include **internal (east-west) traffic between VLANs** to detect unexpected communications and support SOC-relevant observability.

> Notes:  
> - This upgrade enables isolation of IoT, user, and guest devices.  
> - VLAN-aware APs support enterprise-style segmentation and future lab expansions.

---

## Wireless VLAN Considerations

- Access control policies will be enforced via VLAN separation and ACLs on the Cisco switch.  
- Temporary consolidation is documented in `vlan-design.md` and `ip-addressing.md`.  
- Devices requiring monitoring or administrative access will be migrated to their intended VLAN once the EAP610s are deployed.

---

## Summary

- Velop mesh provides temporary wireless service for all devices on Users_Trust VLAN.  
- TP-Link EAP610 upgrade will enable proper VLAN separation for IoT, users, and guests.  
- DHCP and routing remain centralized on the Cisco L3 switch.  
- The wireless design supports lab expansion and enterprise-style segmentation.

---
