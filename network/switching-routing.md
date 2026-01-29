# Switching and Routing

This document outlines the **switching and internal routing design** for the **enterprise-homelab** environment. It provides a clear map of VLAN interfaces, trunking, and routing considerations without exposing sensitive configuration details.

---

## Cisco Catalyst Switch Overview

The **Cisco Catalyst WS-C3560CX-8PC-S** performs:

- VLAN segmentation and isolation  
- L2 switching for access and trunk ports  
- Policy enforcement between VLANs via ACLs  
- Management access and monitoring connectivity

> Notes: Inter-VLAN routing and DHCP are handled by pfSense for centralized control and simplified configuration.

---

## VLAN Interfaces

Each VLAN is defined on the Cisco switch and mapped to the corresponding pfSense interface:

| VLAN ID | Name         | Role / Purpose |
|--------:|--------------|----------------|
| 10      | Mgmt         | Network management (firewall, switch, admin devices) |
| 20      | Security     | SIEM and security tooling |
| 30      | Printers     | Network printers |
| 40      | IoT          | Cameras, smart devices |
| 50      | Users_Trust  | Trusted user devices / Wi-Fi |
| 60      | Guest        | Guest Wi-Fi / internet-only access |

> Notes: VLANs exist on the switch to **enforce segmentation and isolate traffic**. Trunks carry all VLANs between the switch and pfSense.  

---

## Inter-VLAN Routing

- Inter-VLAN routing is handled by **pfSense**, not the Cisco switch.  
- pfSense interfaces provide **default gateways** for each VLAN.  
- Cisco enforces **access policies** using ACLs where necessary for extra internal control.  

> Rationale: Centralizing routing and DHCP on pfSense avoids configuration conflicts and ensures consistent monitoring and security enforcement.

---

## Access and Security Considerations

- **Mgmt VLAN (10):** Only administrative devices have access.  
- **Security VLAN (20):** Isolated for monitoring infrastructure; receives logs and alerts.  
- **Printers VLAN (30):** Accessible from authorized VLANs as needed.  
- **IoT VLAN (40):** Restricted lateral movement; limited access to sensitive VLANs.  
- **Users_Trust VLAN (50):** General user traffic; temporary wireless endpoints are placed here.  
- **Guest VLAN (60):** Internet-only access; no access to internal VLANs.

> Notes: ACLs on the switch are applied for additional segmentation and will be updated as wireless VLAN separation is implemented.

---

## DHCP Services

- DHCP is now **centrally managed by pfSense** for all VLANs.  
- Reserved IPs are configured for critical devices (SIEM, printers).  
- Static IPs are used for infrastructure devices (Netgate, Cisco switch management).  

---

## Summary

- The Cisco switch enforces **VLAN segmentation and ACL-based policy control**.  
- pfSense handles **inter-VLAN routing and DHCP**, providing default gateways for each VLAN.  
- VLANs and trunking define the network topology for isolation and monitoring.  
- Access rules are applied to minimize lateral movement and enforce operational roles.

---
