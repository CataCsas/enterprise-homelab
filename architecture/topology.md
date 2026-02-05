# Network Topology

This document describes the logical and physical topology of the enterprise-style homelab. The environment is designed to resemble a small enterprise network with clear separation between edge security, switching, wireless access, and monitoring systems. The topology prioritizes visibility, segmentation, and operational clarity over complexity.

---

## High-Level Logical Topology

```
[ Internet / ISP ]
        |
[ pfSense (Netgate SG-2100) ]
        |
VLAN-Trunked L2 Network
        |
[ Cisco Catalyst 3560CX ]
        |
------------------------------------------------------
  |        |        |        |        |            |
Mgmt   Security  Printers   IoT   Users_Trust    Guest
VLAN10  VLAN20    VLAN30   VLAN40    VLAN50     VLAN60
```

- pfSense handles all inter-VLAN routing and firewall enforcement.
- Cisco Catalyst switch operates as a Layer 2 access switch with VLAN segmentation.
- VLANs are isolated based on function and trust level.
- Wireless clients currently reside in the Users_Trust VLAN; VLAN-aware WiFi is planned for future deployment.

---

## Physical Topology Overview

- **ISP Router → pfSense (WAN)**  
  Provides upstream internet connectivity.

- **pfSense (LAN) → Cisco Catalyst 3560CX (Trunk)**  
  Carries all VLANs. pfSense enforces routing, access control, and firewall policy.

- **Cisco Catalyst → End Devices**
  - Wired endpoints connect to access ports per VLAN assignment.
  - Wireless access points connect to trunk or L2 ports; currently bridged into Users_Trust VLAN.

- **Wireless Clients**
  - Consumer mesh operating in bridge mode.
  - VLAN-aware SSIDs planned for enterprise-style segmentation.

---

## Component Roles

### Edge Firewall (pfSense / Netgate SG-2100)
- Internet gateway.
- NAT and perimeter firewall.
- Inter-VLAN routing and access control.
- Central point for all policy enforcement, including east–west traffic.
- Pre-secured future VLANs (IoT / Guest) are defined and blocked.

### Core / Access Switching (Cisco Catalyst WS-C3560CX-8PC-S)
- Layer 2 VLAN enforcement.
- Trunking to pfSense.
- Access port assignment.
- Central aggregation point for monitoring and logging.

### Wireless Access Layer
- Temporary consumer mesh in bridge mode.
- Provides network access without routing or VLAN separation.
- VLAN-aware SSIDs planned for enterprise-style segmentation.

### Security Monitoring Host
- Linux-based SIEM host deployed in Security VLAN.
- Collects logs and telemetry from all VLANs.
- Isolated from user and guest traffic.

---

## Design Characteristics

- Single edge firewall for centralized policy enforcement.
- Layer 2 switching for endpoint segmentation.
- Functional VLAN separation to reduce attack surface and lateral movement.
- Pre-secured dormant VLANs for future expansion (IoT and Guest).
- Visibility-first approach to support SOC-style monitoring.

---

## Current State vs Future State

**Current State**
- pfSense performs all inter-VLAN routing and firewall enforcement.
- Cisco Catalyst acts as L2 switch with VLAN segmentation.
- Wireless clients temporarily consolidated in Users_Trust VLAN.
- Security monitoring host operational in Security VLAN.
- Future VLANs exist but are pre-secured and inactive.

**Future State**
- VLAN-aware enterprise WiFi access points.
- Dedicated IoT and Guest networks.
- Expanded server infrastructure (e.g., Active Directory, centralized authentication).
- Enhanced logging, alerting, and access controls.

This topology is intentionally simple, auditable, and aligned with enterprise and SOC practices. Additional complexity is introduced only when it provides clear operational or security benefit.

---
