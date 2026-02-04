# Future Improvements

This document outlines planned enhancements to the **enterprise-homelab** environment. The focus is on expanding detection, visibility, and incident response capabilities in a controlled and repeatable manner.

All future work builds on an established foundation of VLAN segmentation, centralized routing, and explicit inter-VLAN firewall policy enforcement.

---

## Detection & Monitoring

Planned enhancements include:

- Expanding **SIEM coverage** as additional devices and VLANs are activated.  
- Developing **custom detection rules** for events such as authentication failures, policy violations, and unexpected network behavior.  
- Refining alert logic to prioritize actionable events and reduce noise.  
- Validating log completeness and consistency across infrastructure components.

---

## Network Traffic Inspection

Future work will introduce deeper traffic visibility:

- Enable and tune **IDS/IPS capabilities** (e.g., Suricata) at the firewall.  
- Monitor selected east–west traffic paths for unexpected protocols or destinations.  
- Validate IDS alerts and firewall denies through SIEM ingestion and analysis.  

Inspection will be introduced incrementally to avoid unnecessary performance or alerting overhead.

---

## Incident Response Practice

Incident response workflows will be exercised to validate detection and containment:

- Simulate policy violations or misbehaving endpoints (e.g., IoT or user devices).  
- Practice alert triage, scope assessment, and containment actions such as firewall rule adjustments or VLAN isolation.  
- Document outcomes and lessons learned to improve repeatability and response quality.

---

## Identity & Access Controls

Future improvements will strengthen administrative access security:

- Implement **multi-factor authentication** for administrative interfaces where supported.  
- Enforce separation between administrative and non-privileged accounts.  
- Increase visibility into privileged actions through logging and review.

---

## Wireless Segmentation Expansion

Once VLAN-aware access points are deployed:

- Activate **VLAN 40 (IoT)** and **VLAN 60 (Guest)** with pre-defined firewall policies.  
- Separate SSIDs by trust level and function.  
- Validate isolation and access restrictions through testing and monitoring.

---

## Configuration & Change Management

To preserve stability and clarity:

- Continue tracking firewall, switch, and SIEM configuration changes.  
- Periodically review segmentation and access rules for correctness and drift.  
- Update documentation alongside infrastructure changes to reflect current state.

---

## Summary

Planned improvements focus on:

- Expanding detection and monitoring in a controlled, SOC-aligned manner.  
- Introducing traffic inspection and validating east–west visibility.  
- Practicing incident response using realistic scenarios.  
- Strengthening identity controls and wireless segmentation.  
- Maintaining disciplined documentation and change tracking.

These enhancements reflect a deliberate progression from **secure architecture** to **operational security practice**.

---
