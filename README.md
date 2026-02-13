# Enterprise Homelab

This repository documents the design and evolution of an enterprise-style home lab focused on **network segmentation, security monitoring, and SOC-aligned operational practices**.

The lab simulates real-world enterprise infrastructure with an emphasis on clear architecture, controlled traffic flows, and visibility into system and network activity.

---

## Lab Overview

The environment is built using:

- **pfSense** as the edge firewall, inter-VLAN router, and perimeter control
- **Cisco Catalyst switching** for VLAN segmentation, trunking, and access-layer enforcement
- **VLAN-based segmentation** to separate users, infrastructure, IoT, and guest traffic
- **Wazuh SIEM (Linux-based)** for centralized log collection, alerting, and security monitoring

Core infrastructure components (pfSense, Cisco switch, SIEM) use static IP addressing to ensure stable routing, predictable firewall enforcement, and consistent log ingestion.

The lab emphasizes **architectural decisions, security rationale, and operational discipline** aligned with SOC workflows.

---

## Documentation Overview

This repository is supported by structured documentation covering network design, security controls, and monitoring scope.

### Architecture
- [`design-decisions.md`](./architecture/design-decisions.md)
- [`future-improvements.md`](./architecture/future-improvements.md)
- [`topology.md`](./architecture/topology.md)

### Documentation
- [`screenshots.md`](./docs/screenshots.md)

### Network Design
- [`ip-addressing.md`](./network/ip-addressing.md)
- [`switching-routing.md`](./network/switching-routing.md)
- [`vlan-design.md`](./network/vlan-design.md)
- [`wireless.md`](./network/wireless.md)

### Operations
- [`change-management.md`](./operations/change-management.md)
- [`lessons-learned.md`](./operations/lessons-learned.md)

### Security
- [`logging-scope.md`](./security/logging-scope.md)
- [`siem-overview.md`](./security/siem-overview.md)
- [`threat-model.md`](./security/threat-model.md)

---

## Goals and Scope

This lab is intended to:

- Practice **enterprise-style network segmentation**
- Develop familiarity with **security telemetry and log analysis**
- Support **incident detection, investigation, and response concepts**
- Maintain clear, repeatable technical documentation

As the environment evolves, changes are documented with an emphasis on clarity, traceability, and operational relevance.

---

## Status

Current implementation includes:

- Static IP assignment for core infrastructure (pfSense, Cisco management, SIEM)  
- Wired VLAN segmentation (Management, Security, Users, Printers)  
- Stateful firewall policy with restricted inter-VLAN access  
- SIEM positioned in dedicated monitoring VLAN  

Planned next phases:

- Wireless VLAN segmentation  
- Advanced Wazuh alert simulation and rule tuning  
- Detection case studies and incident response documentation  

---
