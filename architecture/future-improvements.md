# Future Improvements

This document outlines planned enhancements to the **enterprise-homelab** environment. The focus is on expanding detection, visibility, and incident response capabilities in a controlled and repeatable manner.

All future work builds on an established foundation of VLAN segmentation, centralized routing, static infrastructure addressing, and explicit inter-VLAN firewall policy enforcement.

The next phase of development transitions the lab from **secure architecture implementation** to **operational detection engineering and incident response practice**.

---

## Detection Engineering & Monitoring Expansion

Planned enhancements include:

- Expanding **Wazuh SIEM coverage** as additional devices and VLANs are activated.  
- Developing and tuning **custom detection rules** for:
  - Authentication failures and brute-force attempts  
  - Lateral movement indicators  
  - Policy violations between VLAN trust zones  
  - Suspicious outbound connections  
- Mapping selected alerts to relevant **MITRE ATT&CK techniques** to reinforce SOC alignment.
- Refining alert severity and threshold logic to reduce false positives.
- Validating log completeness and source attribution across infrastructure components.

Each detection enhancement will include validation steps and documented outcomes.

---

## Detection Case Studies

The lab will include structured detection scenarios documented as case studies:

- Authentication anomaly simulation  
- Unauthorized cross-VLAN access attempt  
- Suspicious service exposure or port scan activity  
- Misconfigured or compromised IoT behavior  

Each case study will document:
- Initial alert source  
- Triage process  
- Log correlation steps  
- Root cause determination  
- Containment decision  
- Lessons learned  

This approach emphasizes repeatable SOC-style investigation workflows rather than ad hoc log review.

---

## Network Traffic Inspection

Future work will introduce deeper traffic visibility:

- Enable and tune **Suricata IDS/IPS** on pfSense.  
- Monitor selected east–west traffic paths for unexpected protocols or destinations.  
- Validate IDS alerts and firewall denies through SIEM ingestion and correlation.  
- Evaluate performance impact and alert noise levels before expanding inspection scope.

Inspection will be introduced incrementally to avoid unnecessary performance or alerting overhead.

---

## Incident Response Practice

Incident response workflows will be exercised to validate detection and containment:

- Simulate policy violations or misbehaving endpoints (e.g., IoT or user devices).  
- Practice alert triage, scope assessment, and containment actions such as:
  - Firewall rule adjustments  
  - VLAN isolation  
  - Service restriction  
- Document investigative reasoning and decision-making process.

The objective is to build structured response discipline aligned with SOC operations.

---

## Identity & Access Controls

Future improvements will strengthen administrative access security:

- Implement **multi-factor authentication** for administrative interfaces where supported.  
- Enforce separation between administrative and non-privileged accounts.  
- Increase visibility into privileged actions through centralized logging and review.  
- Evaluate log retention and audit review processes for completeness.

---

## Wireless Segmentation Expansion

Once VLAN-aware access points are deployed:

- Activate **VLAN 40 (IoT)** and **VLAN 60 (Guest)** with pre-defined firewall policies.  
- Separate SSIDs by trust level and function.  
- Validate isolation and access restrictions through controlled testing.  
- Confirm SIEM visibility across newly segmented wireless networks.

---

## Metrics & Validation Goals

To maintain measurable progress, future phases will track:

- Number of active monitored log sources  
- Number of custom detection rules implemented  
- False-positive reduction improvements over time  
- Number of documented detection case studies  
- Verification of log ingestion across all active VLANs  

This ensures progress is operationally meaningful rather than configuration-focused.

---

## Configuration & Change Management

To preserve stability and clarity:

- Continue tracking firewall, switch, and SIEM configuration changes.  
- Periodically review segmentation and access rules for correctness and drift.  
- Validate monitoring coverage after major infrastructure adjustments.  
- Update documentation alongside infrastructure changes to reflect current state.

---

## Summary

Planned improvements focus on:

- Expanding detection engineering in a structured, SOC-aligned manner.  
- Introducing IDS visibility and validating east–west monitoring.  
- Practicing documented incident response workflows.  
- Strengthening identity controls and wireless segmentation.  
- Maintaining disciplined documentation and change tracking.  

These enhancements reflect a deliberate progression from:

**Secure Network Architecture → Stabilized Infrastructure Baseline → Operational Detection & Response Practice**

The lab’s long-term objective is to simulate not only enterprise network design, but enterprise security operations maturity.

---
