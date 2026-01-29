# Wireless Network

This document outlines the wireless network design for the **enterprise-homelab** environment, including the current temporary setup and planned upgrades.

---

## Temporary Wireless Deployment

- A **Velop mesh** provides wireless coverage temporarily.  
- All wireless endpoints, including IoT devices, are currently consolidated on **VLAN 50 – Users_Trust**.  
- IP addressing follows the VLAN DHCP scheme from **pfSense**.  
- The Velop operates in **bridge mode**, leaving routing, inter-VLAN access, and DHCP to pfSense.  
- The Cisco switch enforces VLAN segmentation and ACLs for internal control.

> Notes:  
> - This temporary setup simplifies connectivity while maintaining basic internal segmentation.  
> - Traffic monitoring and logging are handled centrally by the SIEM host.

---

## Planned Wireless Upgrade

- **TP-Link EAP610** access points will replace the Velop mesh.  
- VLAN tagging will separate wireless traffic into:  
  - **VLAN 40 – IoT**  
  - **VLAN 50 – Users_Trust**  
  - **VLAN 60 – Guest**  
- Each SSID will map to its respective VLAN for proper segmentation.  
- **pfSense** will continue providing DHCP and routing between VLANs where allowed.  
- Future monitoring will include **east-west traffic between VLANs** to detect unexpected communications and support SOC-relevant observability.

> Notes:  
> - This upgrade enables isolation of IoT, user, and guest devices.  
> - VLAN-aware APs support enterprise-style segmentation and future lab expansions.  
> - ACLs on the Cisco switch will enforce internal access restrictions.

---

## Wireless VLAN Considerations

- Access control policies are enforced via VLAN separation and switch ACLs.  
- Temporary consolidation is documented in [`vlan-design.md`](./network/vlan-design.md) and [`ip-addressing.md`](./network/ip-addressing.md).  
- Devices requiring monitoring or administrative access will be migrated to their intended VLAN once the EAP610s are deployed.

---

## Summary

- Velop mesh provides temporary wireless service for all devices on Users_Trust VLAN.  
- TP-Link EAP610 upgrade will enable proper VLAN separation for IoT, users, and guests.  
- **pfSense** centralizes DHCP and routing, while the Cisco switch enforces VLAN segmentation.  
- The wireless design supports lab expansion and enterprise-style segmentation.

---
