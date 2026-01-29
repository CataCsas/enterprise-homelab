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

| Date       | Change Description                               | Affected Components        | Outcome |
|-----------|--------------------------------------------------|---------------------------|---------|
| 2026-01-26 | L3 routing and DHCP moved to pfSense           | pfSense, Cisco switch     | VLAN interfaces created on pfSense; DHCP pools enabled; firewall rules applied; trunk and access ports verified; SIEM and Velop clients tested for connectivity and correct IP assignment |
| 2026-01-22 | Replaced USB console cable to resolve lag       | Cisco switch              | OIKWAN USB→RJ45 cable with FT232 chip tested for FTDI driver compatibility; used for VLAN configuration; console sessions fully stable and smooth |
| 2026-01-19 | Console access and pre-change validation        | Cisco switch              | Verified USB console, IOS version, licensing, VLANs, and interface usage; observed session lag during extended console activity |
| 2026-01-19 | VLAN 30 creation and port assignment            | Cisco switch              | VLAN 30 Printers created; Gi0/7 and Gi0/8 assigned; verified with 'show vlan brief' and 'show interfaces status'; prior console lag noted before cable replacement |

> Notes:  
> - Tracking ensures reproducibility, troubleshooting support, and a clear history of lab evolution.  
> - Chronological order highlights dependencies and shows how issues (like console lag) were resolved.

---

## Summary

- Structured change management reduces the risk of misconfiguration or downtime.  
- All changes are documented, verified, and traceable.  
- Future modifications will follow the same process to maintain a professional, enterprise-style approach.
