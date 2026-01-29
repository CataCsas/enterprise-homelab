# Future Improvements

This document outlines planned enhancements to the **enterprise-homelab** environment. The focus is on improving detection, monitoring, and incident response capabilities in a structured, practical way.

---

## Detection & Monitoring

Planned enhancements include:

- Adding **custom SIEM rules** for relevant events, such as authentication failures and unauthorized access attempts.  
- Refining alerts to ensure they are actionable and reduce noise.  
- Expanding coverage to include additional endpoints as VLAN separation and new devices are introduced.

---

## Incident Response Practice

Incident response workflows will be periodically exercised to validate detection and containment processes:

- Simulate a misbehaving IoT device or policy violation.  
- Practice alert analysis, scope determination, and containment actions, such as firewall rule changes or VLAN-based isolation.  
- Document findings and lessons learned to improve reproducibility and visibility.

---

## Identity & Access

Future improvements will strengthen access controls:

- Implement **MFA using hardware security keys** for administrative accounts.  
- Separate administrative and non-privileged accounts.  
- Log and review privileged actions where possible.

---

## Internal Traffic Visibility

Plans include improving visibility into inter-VLAN communications:

- Monitor unexpected communication paths and protocol usage between VLANs.  
- Log denied access attempts for analysis and review to support detection of lateral movement.

---

## Configuration & Change Management

To maintain clarity and reproducibility:

- Track firewall and switch configuration changes.  
- Periodically review VLAN and access rules.  
- Update documentation alongside infrastructure changes.

---

## Summary

The planned improvements focus on:

- Strengthening monitoring and detection, including **alert tuning and coverage validation**.  
- Practicing **incident response** and verifying **inter-VLAN visibility**.  
- Improving access control and internal segmentation.  
- Maintaining documentation and **change tracking** for reproducibility.

These steps reflect a structured, security-focused approach consistent with learning and operational practice in a SOC-like environment.

---
