# Design Decisions

This document outlines the key architectural and operational decisions made during the design of the **enterprise-homelab** environment. The goal of this lab is to simulate enterprise-style network segmentation, monitoring, and security workflows while remaining practical within home infrastructure constraints.

Decisions documented here prioritize **clarity, defensibility, and alignment with real-world SOC environments**, rather than maximum feature complexity.

---

## Layered Network Architecture

### Edge Firewall (pfSense on Netgate SG-2100)

The Netgate SG-2100 running pfSense is positioned as the **edge firewall and internet gateway**.

**Rationale:**
- Clear separation between perimeter security and internal routing
- pfSense provides enterprise-grade firewalling, NAT, and inspection features

pfSense is intentionally **not used for inter-VLAN routing** in order to keep internal traffic visibility and control within the switching layer.

---

### Internal Routing at the Switch (Cisco Catalyst 3560CX)

The Cisco Catalyst WS-C3560CX-8PC-S functions as a **Layer 3 switch**, performing:

- Inter-VLAN routing (SVIs)
- Default gateway services for internal networks
- DHCP services for client segments

**Rationale:**
- Reduces load and complexity on the firewall
- Enables fine-grained control and visibility at the switching layer
- Reinforces hands-on experience with Cisco IOS routing concepts

This design reflects environments where routing is distributed closer to endpoints rather than centralized at the firewall.

---

## VLAN Segmentation Strategy

The network is segmented using function-based VLANs:

- **VLAN 10 – Mgmt**
- **VLAN 20 – Security**
- **VLAN 30 – Printers**
- **VLAN 40 – IoT**
- **VLAN 50 – Users_Trust**
- **VLAN 60 – Guest**

**Rationale:**
- Limits broadcast domains
- Reduces lateral movement risk
- Enables policy-based access control
- Aligns with Zero Trust segmentation principles

Segmentation decisions are driven by **device trust level and operational role**, not by physical location.

---

## Management and Security Separation

Management infrastructure (network devices, SIEM host) is isolated from user endpoints.

**Rationale:**
- Prevents administrative interfaces from being exposed to end-user networks
- Aligns with least-privilege access principles
- Reflects SOC and NOC separation practices in enterprise environments

Administrative access is expected to occur from controlled endpoints only.

---

## DHCP Placement and Addressing

DHCP services are provided by the **Cisco Catalyst switch** rather than the firewall.

**Rationale:**
- Keeps network services close to the endpoints
- Simplifies firewall rule sets
- Reinforces IOS DHCP configuration experience

Static IP addressing or DHCP reservations are used for:
- Network infrastructure devices
- Printers
- SIEM host

Dynamic addressing is used for general user and guest endpoints.

---

## Wireless Design Considerations

Wireless access is currently provided via a consumer-grade mesh system operating in **bridge mode**.

**Current state:**
- Wireless clients are temporarily placed in the **Users_Trust VLAN**
- IoT devices are also temporarily consolidated due to wireless limitations

**Planned evolution:**
- Migration to enterprise-grade access points (e.g., TP-Link EAP series)
- VLAN-aware SSIDs
- Separation of IoT and user wireless traffic

This phased approach reflects real-world constraints and incremental network upgrades.

---

## SIEM Placement and Scope

A dedicated Linux-based SIEM host is deployed within the **Security VLAN**.

**Rationale:**
- Isolates monitoring infrastructure from production traffic
- Prevents unnecessary exposure to user or guest networks
- Aligns with SOC monitoring architectures

The SIEM is intended to ingest logs from:
- Network devices
- Servers (future)
- Endpoints (future)

Scope expansion is documented separately to maintain clear operational boundaries.

---

## Documentation and Security Posture

This repository intentionally focuses on:
- Architecture
- Design rationale
- Operational intent

---

## Incremental Build Philosophy

The homelab is designed to evolve incrementally.

**Key principles:**
- Design
- Implement
- Document decisions

Future enhancements are tracked separately to avoid conflating current-state design with planned capabilities.

---
