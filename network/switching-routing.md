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

- DHCP is centrally managed by pfSense for all VLANs.  
- Reserved IPs are configured for critical devices (SIEM, printers).  
- Static IPs are used for infrastructure devices (Netgate, Cisco switch management).  

---

## Summary

This design delineates responsibilities clearly between layers:

- **Cisco Catalyst (L2):** Enforces VLAN isolation, access port policies, and ACL-based traffic constraints.  
- **pfSense (L3):** Handles inter-VLAN routing, DHCP, and centralized default gateway services.  
- VLAN trunking maintains consistent connectivity without exposing internal routing complexity.  
- ACLs on the switch complement firewall rules to reduce risk and enforce functional separation.  

The approach ensures **clear operational boundaries, predictable routing, and disciplined switching enforcement**, independent of addressing or higher-level topology details.

---
