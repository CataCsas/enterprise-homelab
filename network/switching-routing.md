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
| 40      | IoT          | Cameras, smart devices (pre-secured, inactive) |
| 50      | Users_Trust  | Trusted user devices / temporary Wi-Fi endpoints |
| 60      | Guest        | Guest Wi-Fi / internet-only access (pre-secured, inactive) |

> Notes: VLANs exist on the switch to **enforce segmentation and isolate traffic**. Trunks carry all VLANs between the switch and pfSense.  

---

## Inter-VLAN Routing

- Inter-VLAN routing is handled by **pfSense**, not the Cisco switch.  
- pfSense interfaces provide **default gateways** for each VLAN.  
- Cisco enforces **access policies** using ACLs for additional internal control.  

> Rationale: Centralizing routing and DHCP on pfSense avoids configuration conflicts and ensures consistent monitoring, security enforcement, and alignment with SOC workflows.

---

## Access and Security Considerations

- **Mgmt VLAN (10):** Only administrative devices have access.  
- **Security VLAN (20):** Isolated for monitoring infrastructure; receives logs and alerts.  
- **Printers VLAN (30):** Accessible from authorized VLANs as needed.  
- **IoT VLAN (40):** Restricted lateral movement; limited access to sensitive VLANs; pre-secured.  
- **Users_Trust VLAN (50):** General user traffic; temporary wireless endpoints are placed here.  
- **Guest VLAN (60):** Internet-only access; no access to internal VLANs; pre-secured.  

> Notes: ACLs on the switch complement pfSense firewall rules and will support VLAN-aware wireless separation when deployed.

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
- Switch ACLs and pfSense firewall rules work together to **minimize lateral movement** and enforce operational roles.  
- Pre-secured VLANs enable safe expansion for future IoT and Guest Wi-Fi networks.

---
