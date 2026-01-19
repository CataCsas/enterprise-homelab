# Change Management

This document outlines the process for managing changes within the **enterprise-homelab** environment. It ensures that modifications are planned, documented, and traceable, minimizing risks to network and system stability.

---

## Change Planning

- All planned changes are reviewed before implementation.  
- Changes include:
  - VLAN creation or modification
  - Device configuration updates (firewall, switch, SIEM, printers)
  - Network service additions or removals
- Impact and dependencies are considered, and potential risks are noted.

---

## Implementation Process

1. **Preparation**  
   - Backup existing configurations where applicable (pfSense, Cisco, SIEM host).  
   - Document the current state and intended changes in Markdown files.  

2. **Execution**  
   - Apply changes during low-activity periods where possible.  
   - Use console or management interfaces to implement configurations.  

3. **Verification**  
   - Test connectivity, VLAN segmentation, and device functionality.  
   - Verify logging and monitoring coverage in the SIEM.  

4. **Documentation**  
   - Record each change in this repository with:
     - Description
     - Date and rationale
     - Outcome and verification notes

---

## Change Tracking

| Date       | Change Description                     | Affected Components | Outcome |
|-----------|----------------------------------------|------------------|---------|
| 2026-01-19 | Console access and pre-change validation | Cisco switch | Verified USB console, IOS version, licensing, VLANs, and interface usage; observed expected PnP messages and lag during session |
| 2026-01-19 | VLAN 30 creation and port assignment | Cisco switch | VLAN 30 Printers created; Gi0/7 and Gi0/8 assigned; verified with 'show vlan brief' and 'show interfaces status'; console lag persisted |

> Notes:  
> - Tracking ensures reproducibility and supports troubleshooting.  
> - Historical records track lab evolution.

---

## Summary

- Structured change management reduces the risk of misconfiguration or downtime.  
- Changes are documented, verified, and traceable.  
- Future modifications follow the same process to maintain a professional, enterprise-style approach.

---
