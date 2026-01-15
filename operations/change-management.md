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
| YYYY-MM-DD | Example: Added VLAN 40 for IoT devices | Cisco switch      | Verified connectivity and SIEM logging |

> Notes:  
> - Tracking ensures reproducibility and supports troubleshooting.  
> - Historical records track lab evolution.

---

## Summary

- Structured change management reduces the risk of misconfiguration or downtime.  
- Changes are documented, verified, and traceable.  
- Future modifications follow the same process to maintain a professional, enterprise-style approach.

---
