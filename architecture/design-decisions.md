# Design Decisions

This document outlines the key architectural and operational decisions made during the design of the **enterprise-homelab** environment. The goal of this lab is to simulate enterprise-style network segmentation, monitoring, and security workflows while remaining practical within home infrastructure constraints.

Decisions documented here prioritize **clarity, defensibility, and alignment with real-world SOC and enterprise network environments**, rather than maximum feature complexity.

---

## Layered Network Architecture

### Edge Firewall, Routing, and Policy Enforcement (pfSense on Netgate SG-2100)

The Netgate SG-2100 running pfSense is positioned as the **edge firewall, internet gateway, inter-VLAN router, and primary policy enforcement point**.

pfSense is responsible for:
- Inter-VLAN routing
- Default gateway services for all internal networks
- DHCP services
- NAT and perimeter firewall enforcement
- East–west traffic control between VLANs

**Rationale:**
- Centralizes routing and security policy at a single, auditable control point  
- Enables explicit, least-privilege access control between trust zones  
- Simplifies troubleshooting and visibility into traffic flows  
- Aligns with enterprise designs where firewalls act as both routers and policy engines  

This design was selected after evaluating Layer 3 routing on the switching platform and determining that centralized routing and enforcement on pfSense provided greater reliability, control, and long-term maintainability for this environment.

---

### Internal Switching and Segmentation (Cisco Catalyst 3560CX)

The Cisco Catalyst WS-C3560CX-8PC-S functions as a **Layer 2 access switch**, providing:

- VLAN segmentation
- Trunking to the firewall
- Access port assignment and enforcement
- Enterprise-style interface configuration and operational discipline

**Rationale:**
- The installed IOS image does not support the required Layer 3 routing features  
- Attempted SVI-based routing commands were unavailable  
- Centralizing routing and policy enforcement on the firewall avoids split responsibility  

This mirrors common enterprise access-layer designs where:
- Routing and security decisions occur upstream  
- Access switches focus on segmentation and endpoint control  
- Layer 3 capabilities are not assumed at every tier  

---

## Firewall Policy and Trust Model

Inter-VLAN communication is governed by an explicit, firewall-centric security model implemented on pfSense.

**Design principles:**
- Default deny by design  
- Access granted by exception, not convenience  
- East–west traffic restricted unless explicitly required  
- No reliance on implicit firewall behavior for security-critical paths  

Each VLAN is treated as a distinct **trust zone**, with access scoped to its operational role.

**Policy characteristics:**
- Explicit IPv4 deny rules are used to make intent visible and auditable  
- IPv6 is explicitly disabled across all VLANs to prevent unintended exposure  
- Internet access is allowed only where required  
- Internal network access is tightly constrained using alias-based policy logic  

Firewall rules were fully designed and implemented **before** finalizing static IP assignments or relocating the SIEM, ensuring policy stability and preventing configuration drift.

---

## VLAN Segmentation Strategy

The network is segmented using function-based VLANs:

- **VLAN 10 – Mgmt** (high trust)
- **VLAN 20 – Security** (high trust, scoped)
- **VLAN 30 – Printers** (restricted, low capability)
- **VLAN 40 – IoT** (untrusted, future)
- **VLAN 50 – Users_Trust** (mixed trust)
- **VLAN 60 – Guest** (untrusted, future)

**Rationale:**
- Limits broadcast domains  
- Reduces lateral movement risk  
- Enables policy-based access control  
- Aligns with Zero Trust segmentation principles  

Segmentation decisions are driven by **device trust level and operational role**, not physical location.

---

## Management and Security Separation

Management and security infrastructure is isolated from user, IoT, and guest networks.

**Rationale:**
- Prevents administrative interfaces from being exposed to end-user traffic  
- Enforces least-privilege access principles  
- Reflects SOC and NOC separation practices  

Administrative access is expected to originate only from controlled and trusted environments.

---

## DHCP Placement and Addressing

DHCP services are provided centrally by **pfSense**, with scopes defined per VLAN.

**Rationale:**
- Avoids split-brain DHCP scenarios  
- Keeps addressing aligned with routing and firewall policy  
- Simplifies VLAN-aware network management  

Static IP addressing or DHCP reservations are used for:
- Network infrastructure devices  
- Printers  
- SIEM host  

Dynamic addressing is used for general user, IoT, and guest endpoints.

---

## Wireless Design Considerations

Wireless access is currently provided via a consumer-grade mesh system operating in **bridge mode**.

**Current state:**
- Wireless clients reside temporarily in the **Users_Trust VLAN**  
- IoT devices are consolidated due to wireless limitations  

**Planned evolution:**
- Migration to VLAN-aware, enterprise-grade access points  
- Dedicated SSIDs per trust zone  
- Full separation of user, IoT, and guest wireless traffic  

This phased approach reflects realistic upgrade paths found in production environments.

---

## SIEM Placement and Scope

A dedicated Linux-based SIEM host is deployed within the **Security VLAN**.

**Rationale:**
- Isolates monitoring infrastructure from general user traffic  
- Limits exposure while preserving visibility  
- Aligns with enterprise SOC architectures  

Firewall policy design and validation were completed prior to final SIEM relocation to ensure monitoring infrastructure is introduced into a stable, well-defined security posture.

The SIEM scope is intended to expand incrementally as additional infrastructure is deployed and validated.

---

## Documentation and Security Posture

This repository documents:
- Architectural intent  
- Design rationale  
- Operational boundaries  

Sensitive implementation details are intentionally excluded. The focus is on **defensible design**, not configuration disclosure.

---

## Incremental Build Philosophy

The homelab evolves incrementally following a consistent pattern:

- Design  
- Implement  
- Validate  
- Document  

Future enhancements are tracked separately to avoid conflating current-state architecture with planned capabilities.

---
