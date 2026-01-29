# Design Decisions

This document outlines the key architectural and operational decisions made during the design of the **enterprise-homelab** environment. The goal of this lab is to simulate enterprise-style network segmentation, monitoring, and security workflows while remaining practical within home infrastructure constraints.

Decisions documented here prioritize **clarity, defensibility, and alignment with real-world SOC and enterprise network environments**, rather than maximum feature complexity.

---

## Layered Network Architecture

### Edge Firewall and Routing (pfSense on Netgate SG-2100)

The Netgate SG-2100 running pfSense is positioned as the **edge firewall, internet gateway, and inter-VLAN router**.

pfSense is responsible for:
- Inter-VLAN routing
- Default gateway services for all internal networks
- DHCP services
- NAT and perimeter firewall enforcement

**Rationale:**
- Centralizes routing and security enforcement at a single, well-defined control point
- Simplifies troubleshooting and traffic flow visibility
- Aligns with common enterprise designs where routing is handled by the firewall when L3 switching is unavailable or undesired

This decision was made after evaluating Layer 3 routing on the switch platform and determining that centralized routing on pfSense was the most reliable and maintainable approach for this environment.

---

### Internal Switching and Segmentation (Cisco Catalyst 3560CX)

The Cisco Catalyst WS-C3560CX-8PC-S functions as a **Layer 2 access switch**, providing:

- VLAN segmentation
- Trunking to the firewall
- Access port assignment and enforcement
- Enterprise-style interface configuration and operational discipline

**Rationale:**
- The switch platform and IOS image did not support the required Layer 3 routing features
- Attempted L3 configuration commands were unavailable, preventing SVI-based routing
- Maintaining VLAN enforcement at Layer 2 still provides strong segmentation and mirrors many real-world access-layer deployments

This design reflects environments where:
- Routing is centralized at the firewall
- Access switches focus on segmentation and endpoint control
- Layer 3 switching is not universally available across all hardware tiers

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

Management and security infrastructure (network devices, SIEM host) is isolated from user and guest networks.

**Rationale:**
- Prevents administrative interfaces from being exposed to end-user networks
- Enforces least-privilege access principles
- Reflects SOC and NOC separation practices in enterprise environments

Administrative access is expected to originate from controlled and trusted endpoints only.

---

## DHCP Placement and Addressing

DHCP services are provided centrally by **pfSense**, with scopes defined per VLAN.

**Rationale:**
- Avoids split-brain DHCP scenarios
- Keeps network services aligned with routing and firewall policy
- Simplifies VLAN-aware address management

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
- Full separation of user, IoT, and guest wireless traffic

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

Scope expansion is tracked separately to maintain operational clarity.

---

## Documentation and Security Posture

This repository focuses on documenting:
- Architectural intent
- Design rationale
- Operational boundaries

---

## Incremental Build Philosophy

The homelab is designed to evolve incrementally.

**Key principles:**
- Design
- Implement
- Document decisions

Future enhancements are tracked separately to avoid conflating current-state design with planned capabilities.

---
