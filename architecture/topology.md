# Network Topology

This document describes the logical and physical topology of the enterprise-style homelab. The environment is designed to resemble a small enterprise network with clear separation between edge security, routing, switching, wireless access, and monitoring systems.

The topology prioritizes visibility, segmentation, and operational clarity over complexity.

---

## High-Level Logical Topology

```
[ Internet / ISP ]
        |
[ pfSense (Netgate SG-2100) ]
        |
   Routed Transit Network
        |
[ Cisco Catalyst 3560CX ]
   (Layer 3 Switching)
        |
------------------------------------------------------
  |        |        |        |        |            |
Mgmt   Security  Printers   IoT   Users_Trust    Guest
VLAN10  VLAN20    VLAN30   VLAN40    VLAN50     VLAN60
```

- The pfSense appliance acts as the **edge firewall and internet gateway**.
- The Cisco Catalyst switch performs **inter-VLAN routing** using Layer 3 SVIs.
- Endpoints are segmented by function using VLANs.
- Wireless access is bridged into the wired network and treated as an access layer.

---

## Physical Topology Overview

- **ISP Router → pfSense (WAN)**  
  Provides upstream internet connectivity.

- **pfSense (LAN) → Cisco Catalyst 3560CX**  
  Single routed transit connection. pfSense is not aware of individual internal VLANs beyond static routing.

- **Cisco Catalyst → End Devices**
  - Wired endpoints connect directly to access ports.
  - Wireless access point connects as a Layer 2 bridge.

- **Wireless Clients**
  - Consumer mesh access point operating in bridge mode
  - VLAN-aware wireless segmentation planned for a future upgrade

---

## Role of Each Component

### Edge Firewall (pfSense / Netgate SG-2100)
- Internet gateway
- NAT and perimeter firewalling
- Policy enforcement at the network edge
- Separation between trusted internal networks and untrusted external traffic

### Core / Distribution Switching (Cisco Catalyst WS-C3560CX-8PC-S)
- Layer 3 inter-VLAN routing
- VLAN segmentation by function
- Default gateway for internal subnets
- DHCP services for internal networks
- Central aggregation point for monitoring and logging

### Wireless Access Layer
- Consumer mesh access point operating in bridge mode
- Provides wireless connectivity without routing or NAT
- All wireless traffic enters the network at Layer 2
- VLAN-aware SSID segmentation deferred to future enterprise AP deployment

### Security Monitoring Host
- Linux-based SIEM platform
- Deployed in a dedicated security-focused VLAN
- Designed to receive logs and telemetry from multiple network segments

---

## Design Characteristics

- **Single edge firewall** for consistent policy enforcement
- **Layer 3 switching** to reduce unnecessary traffic through the firewall
- **Functional VLAN segmentation** to reduce attack surface and noise
- **Clear trust boundaries** between management, users, IoT, and guest traffic
- **Visibility-first approach** to support SOC-style monitoring and analysis

---

## Current State vs Future State

**Current State**
- Wireless clients temporarily share a trusted VLAN due to access point limitations
- Core routing and segmentation already in place
- SIEM deployed but log ingestion is incremental

**Future State**
- VLAN-aware access points enabling multiple SSIDs
- Dedicated wireless IoT and guest networks
- Expanded server infrastructure (e.g., Active Directory, centralized authentication)
- Enhanced logging and access controls

---

This topology is intentionally simple, auditable, and extensible. Additional complexity is introduced only when it provides clear operational or security benefits.
