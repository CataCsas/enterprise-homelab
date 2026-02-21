# Network Topology

This document describes the logical and physical topology of the enterprise-style homelab. The environment is designed to resemble a small enterprise network with clear separation between edge security, switching, wireless access, and monitoring systems. The topology prioritizes visibility, segmentation, and operational clarity over complexity.

All routing, policy enforcement, and east–west traffic inspection occur at the firewall layer to maintain centralized control and auditable rule management.

---

## High-Level Logical Topology

```
[ Internet / ISP ]
        |
[ pfSense (Netgate SG-2100) ]
        |
802.1Q VLAN Trunk
        |
[ Cisco Catalyst 3560CX ]
        |
------------------------------------------------------
  |        |        |        |        |            |
Mgmt   Security  Printers   IoT   Users_Trust    Guest
VLAN10  VLAN20    VLAN30   VLAN40    VLAN50     VLAN60
```


- pfSense performs all Layer 3 routing and firewall enforcement.
- The Cisco Catalyst operates strictly as a Layer 2 access switch.
- All VLANs are trunked to pfSense via 802.1Q.
- Inter-VLAN communication is explicitly controlled by firewall policy.
- Dormant VLANs (IoT and Guest) are pre-defined and default-deny.

---

## VLAN Architecture

| VLAN | Name         | Purpose                                  | Trust Level |
|------|--------------|-------------------------------------------|-------------|
| 10   | Management   | Infrastructure management interfaces      | High        |
| 20   | Security     | SIEM, monitoring, and security tooling    | High        |
| 30   | Printers     | Network printers and utility devices      | Restricted  |
| 40   | IoT          | IoT and untrusted embedded devices        | Low         |
| 50   | Users_Trust  | Primary workstation and lab devices       | Medium      |
| 60   | Guest        | Internet-only guest access                | Low         |

All VLAN gateways reside on pfSense.  
No Layer 3 switching occurs on the Cisco Catalyst.

---

## Physical Topology Overview

- **ISP Router → pfSense (WAN)**  
  Provides upstream internet connectivity.

- **pfSense (LAN) → Cisco Catalyst 3560CX (802.1Q Trunk)**  
  Carries all defined VLANs.  
  Firewall policies govern all inter-VLAN traffic.

- **Cisco Catalyst → End Devices**
  - Access ports statically assigned per VLAN.
  - Trunk port dedicated to firewall uplink.
  - Optional trunk ports reserved for future VLAN-aware wireless APs.

- **Wireless Access Layer**
  - Current: Consumer mesh operating in bridge mode (Users_Trust VLAN).
  - Planned: VLAN-aware enterprise APs with segmented SSIDs mapped to VLAN40 and VLAN60.

---

## Component Roles

### Edge Firewall (pfSense / Netgate SG-2100)

- Default gateway for all VLANs.
- NAT and perimeter firewall.
- Inter-VLAN routing and east–west policy enforcement.
- Suricata IDS/IPS (planned or staged) for traffic inspection.
- Centralized logging export to Wazuh SIEM.

### Core / Access Switching (Cisco Catalyst WS-C3560CX-8PC-S)

- Layer 2 VLAN segmentation.
- 802.1Q trunk to firewall.
- Static access port assignments.
- Logging enabled for configuration and interface state changes.

### Security Monitoring Host (Security VLAN)

- Linux-based Wazuh SIEM node.
- Static IP addressing.
- Receives:
  - Firewall logs
  - System logs
  - Authentication logs
  - IDS alerts (when enabled)
- Isolated from user and guest VLANs.

### Wireless Infrastructure (Current and Planned)

- Current: Bridge-mode consumer mesh.
- Future:
  - VLAN-aware SSIDs
  - IoT and Guest network activation
  - Controlled east–west access validation
  - SIEM log verification for wireless events

---

## Traffic Flow Model

- North–South traffic:
  - Internet ↔ pfSense ↔ Internal VLANs
  - NAT and firewall inspection at perimeter.

- East–West traffic:
  - VLAN ↔ pfSense ↔ VLAN
  - Explicit firewall rule requirement.
  - Default deny between trust zones.

- Security visibility:
  - Firewall logs exported to SIEM.
  - IDS alerts (future state) ingested and correlated.
  - Cross-VLAN access attempts monitored.

---

## Logging & Visibility Model

- Centralized log aggregation via Wazuh.
- Firewall deny events monitored for policy validation.
- Authentication events monitored for anomaly detection.
- Planned validation of log coverage across all active VLANs.
- Configuration changes tracked for drift detection.

---

## Current State

- pfSense performing all routing and firewall enforcement.
- Cisco Catalyst operating strictly as Layer 2.
- VLAN segmentation implemented and verified.
- Security monitoring host operational in VLAN20.
- Dormant VLAN40 (IoT) and VLAN60 (Guest) defined but inactive.
- Wireless currently consolidated in Users_Trust VLAN.
- Structured detection engineering phase in progress.

---

## Planned Enhancements

- VLAN-aware enterprise wireless deployment.
- Activation of IoT and Guest networks with strict isolation.
- IDS/IPS inspection tuning and validation.
- Expanded detection rule coverage mapped to MITRE ATT&CK.
- Additional infrastructure services (e.g., centralized authentication).
- Formalized change tracking and configuration baselines.

---

## Design Principles

- Centralized Layer 3 control at the firewall.
- Explicit trust boundary enforcement.
- Default-deny inter-VLAN posture.
- Incremental complexity based on operational value.
- Visibility-first architecture aligned with SOC practices.
- Documentation updated alongside infrastructure changes.

---

## Summary

This topology reflects a deliberate enterprise-aligned design:

**Segmentation → Centralized Enforcement → Visibility → Detection Engineering → Incident Response Practice**

The lab prioritizes operational realism over unnecessary complexity, supporting both secure architecture design and structured security operations development.

---
