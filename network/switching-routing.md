# Switching and Routing

This document outlines the Layer 3 switching and inter-VLAN routing design for the **enterprise-homelab** environment. It provides a clear map of VLAN interfaces, default gateways, and routing considerations without exposing sensitive configuration details.

---

## Layer 3 Switch Overview

The **Cisco Catalyst WS-C3560CX-8PC-S** performs:

- VLAN segmentation and isolation
- Inter-VLAN routing
- DHCP services for client VLANs
- Default gateway responsibilities for internal networks

The switch enables **centralized internal routing** while keeping the firewall focused on edge protection.

---

## VLAN Interfaces (SVIs)

Each VLAN has a corresponding **Switched Virtual Interface (SVI)** configured on the Cisco switch:

| VLAN ID | Name         | SVI IP Address     | Role |
|--------:|--------------|-----------------|------|
| 10      | Mgmt         | 192.168.10.2    | Gateway for management network |
| 20      | Security     | 192.168.20.1    | Gateway for security VLAN |
| 30      | Printers     | 192.168.30.1    | Gateway for printer VLAN |
| 40      | IoT          | 192.168.40.1    | Gateway for IoT VLAN |
| 50      | Users_Trust  | 192.168.50.1    | Gateway for trusted user VLAN |
| 60      | Guest        | 192.168.60.1    | Gateway for guest VLAN |

> Notes:  
> - SVI addresses serve as the **default gateway** for devices in each VLAN.  
> - VLAN interfaces are limited to the necessary ports and access to minimize exposure.  

---

## Inter-VLAN Routing

- Routing between VLANs occurs **entirely on the L3 switch**.  
- Policies controlling which VLANs can communicate are enforced via **Access Control Lists (ACLs)**.  
- Temporary routing adjustments are made for lab convenience, e.g., allowing SIEM to reach all monitored VLANs.  

> Rationale: Centralizing internal routing on the switch maintains visibility and control for monitoring and policy enforcement.

---

## Access and Security Considerations

- **Management VLAN (VLAN 10)**: Only devices with administrative responsibilities can access.  
- **Security VLAN (VLAN 20)**: Isolated from general user traffic; receives logs and monitoring data.  
- **Printers (VLAN 30)**: Accessible from authorized VLANs only, based on operational needs.  
- **IoT VLAN (VLAN 40)**: Restricted east-west communication; internet access controlled.  
- **Users_Trust (VLAN 50)**: General user traffic; temporary consolidation of wireless endpoints.  
- **Guest (VLAN 60)**: Internet-only; no access to internal VLANs.

> Notes: Access rules are applied using switch-based ACLs and will evolve as wireless segmentation is implemented.

---

## DHCP Services

- DHCP is provided by the switch for VLANs that require dynamic addressing.  
- Reserved IPs are configured for critical devices (SIEM, printers).  
- Static IPs are used for infrastructure devices (Netgate, Cisco switch management).  

---

## Summary

- All internal routing is centralized on the L3 switch for visibility and policy control.  
- SVIs define default gateways for each VLAN.  
- ACLs enforce separation between VLANs based on operational roles.  
- DHCP is integrated with VLAN interfaces to provide dynamic addressing where appropriate.  

---
