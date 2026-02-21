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
- [`detection-cases/`](./security/detection-cases/)

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

### Infrastructure

- Static IP assignment for core infrastructure (pfSense, Cisco management, SIEM)  
- Wired VLAN segmentation (Management, Security, Users, Printers)  
- Stateful firewall policy with restricted inter-VLAN access  
- Dedicated Security VLAN (VLAN20) for SIEM monitoring  

### Security Monitoring

- Wazuh installed and operational on VLAN20  
- Log ingestion validated from `/var/log/auth.log`  
- Alert correlation and rule validation confirmed  

### Detection Case Studies (Completed)

- **[Detection Case 01 – Failed Sudo Escalation](./security/detection-cases/01-sudo-failure.md)**
  - Validated Rule 5503 (authentication failure)
  - Correlated escalation to Rule 5404 (three failed sudo attempts)
  - Documented SOC triage workflow

- **[Detection Case 02 – Scripted Persistence Simulation](./security/detection-cases/02-scripted-persistence.md)**
  - Simulated account creation and privilege escalation
  - Validated File Integrity Monitoring (FIM) for `/etc/passwd`, `/etc/group`
  - Detected cron-based persistence creation
  - Captured structured `alerts.json` snapshot for reconstruction

### Operational Documentation

- VLAN20 DNS/NTP connectivity incident documented  
- Firewall rule refinement recorded with remediation steps  
- Change management and lessons learned updated  

---

## Planned Next Phases

- Cross-VLAN detection case (centralized monitoring validation)  
- Wireless VLAN segmentation  
- Advanced Wazuh rule tuning and dashboard refinement  
- Structured log analysis and timeline reconstruction exercises  
- DFIR-focused portfolio projects  

---
