# Future Improvements

This document outlines planned enhancements to the **enterprise-homelab** environment. The focus is on expanding detection engineering, traffic visibility, and structured incident response capability in a controlled and repeatable manner.

The lab has progressed beyond initial secure architecture implementation and now includes validated detection case studies. Future work builds on that operational baseline.

---

## Current Detection Baseline

The following capabilities have been validated:

- Successful Wazuh log ingestion from Linux system logs  
- Authentication failure correlation (e.g., repeated failed sudo attempts)  
- Detection of account creation and privilege escalation events  
- File Integrity Monitoring (FIM) validation for sensitive system files  
- Detection of cron-based persistence  
- Structured alert export for timeline reconstruction  

Future improvements expand on this validated foundation.

---

## Detection Engineering Expansion

Planned enhancements include:

- Expanding **Wazuh SIEM coverage** as additional devices and VLANs are activated  
- Developing and tuning **custom detection rules** for:
  - Cross-VLAN policy violations  
  - Suspicious outbound connections  
  - Lateral movement indicators  
  - Excessive authentication anomalies  
- Mapping alerts to relevant **MITRE ATT&CK techniques** to reinforce SOC alignment  
- Refining alert thresholds to reduce noise while preserving signal  
- Validating log completeness and source attribution across infrastructure components  

Each enhancement will include documented validation and outcome analysis.

---

## Cross-VLAN Monitoring Validation

A planned detection case will validate centralized monitoring across segmented networks:

- Trigger security-relevant activity from a user VLAN  
- Confirm ingestion and correlation by the SIEM in the Security VLAN  
- Validate that segmentation does not impair visibility  

This scenario will demonstrate multi-host detection capability in a segmented environment.

---

## Network Traffic Inspection

Future work will introduce deeper traffic visibility:

- Enable and tune **Suricata IDS/IPS** on pfSense  
- Monitor selected east–west traffic paths for unexpected protocols or destinations  
- Validate IDS alerts through SIEM ingestion and correlation  
- Evaluate performance impact and alert volume before expanding inspection scope  

Inspection will be introduced incrementally to preserve stability.

---

## Incident Response Maturity

Incident response workflows will be expanded and formalized:

- Simulate controlled policy violations or misbehaving endpoints  
- Practice structured triage and scope assessment  
- Execute containment steps such as:
  - Firewall rule refinement  
  - VLAN isolation  
  - Service restriction  
- Document investigative reasoning and decision-making steps  

The objective is to reinforce disciplined SOC-style response processes.

---

## Structured Log Analysis & Timeline Reconstruction

Future exercises will include:

- Correlating multiple alert types within defined event windows  
- Reconstructing attack timelines using structured JSON exports  
- Identifying alert clustering patterns and causal relationships  
- Producing concise incident summary reports  

This will bridge detection engineering with entry-level DFIR methodology.

---

## Identity & Access Controls

Planned improvements include:

- Enforcing multi-factor authentication where supported  
- Strengthening separation between privileged and non-privileged accounts  
- Increasing visibility into administrative actions  
- Reviewing log retention and audit completeness  

---

## Wireless Segmentation Expansion

Once VLAN-aware access points are deployed:

- Activate **VLAN 40 (IoT)** and **VLAN 60 (Guest)**  
- Separate SSIDs by trust level  
- Validate isolation and firewall enforcement  
- Confirm SIEM visibility across wireless segments  

---

## Metrics & Validation Goals

To maintain measurable progress:

- Track active monitored log sources  
- Track implemented detection rules  
- Measure reduction in unnecessary alerts  
- Document completed detection case studies  
- Verify log ingestion across all active VLANs  

Progress will be measured by validated monitoring capability, not configuration volume.

---

## Configuration & Change Discipline

To preserve architectural clarity:

- Continue tracking firewall, switch, and SIEM configuration changes  
- Periodically review segmentation and rule sets for drift  
- Revalidate monitoring coverage after infrastructure adjustments  
- Update documentation alongside configuration changes  

---

## Summary

Future enhancements emphasize measurable operational progress and SOC-aligned practice:

- Expand monitored log sources and detection coverage across all VLANs  
- Develop, tune, and validate custom alerting rules  
- Execute structured detection case studies and document investigative workflows  
- Introduce IDS visibility and controlled east–west traffic inspection  
- Strengthen administrative access, identity controls, and segmented wireless networks  
- Maintain disciplined documentation and change management  

This phase shifts the lab from a stabilized infrastructure baseline toward **repeatable detection engineering and incident response practice**, providing a controlled environment for testing, validation, and operational learning.

---
