# Change Management

This document defines the process for planning, implementing, and tracking changes within the **enterprise-homelab** environment. It serves as the authoritative change log to ensure all modifications are documented, verified, and traceable.

---

## Change Planning

- All planned changes are reviewed prior to implementation.  
- Changes may include:
  - VLAN creation or modification
  - Device configuration updates (firewall, switch, SIEM, printers)
  - Network service additions or removals
- Potential impact, dependencies, and risk are evaluated before execution.

---

## Implementation Process

1. **Preparation**
   - Back up existing configurations where applicable (pfSense, Cisco switch, SIEM host).
   - Document the current state and intended changes in repository Markdown files.

2. **Execution**
   - Apply changes during low-activity periods where possible.
   - Use console or management interfaces appropriate to each device.

3. **Verification**
   - Validate connectivity, VLAN segmentation, and device functionality.
   - Confirm log forwarding and monitoring visibility within the SIEM.

4. **Documentation**
   - Record each completed change with:
     - Description
     - Date and rationale
     - Outcome and verification notes

---

## Change Tracking

| Date       | Change Description                                | Affected Components       | Outcome |
|-----------|--------------------------------------------------|---------------------------|---------|
| 2026-02-03 | Final VLAN deployment and baseline validation    | pfSense, Cisco switch, SIEM | All production VLANs (Mgmt, Security, Printers, IoT, Users_Trust, Guest) confirmed operational; inter-VLAN routing validated via pfSense firewall rules; trunk and access ports verified; DHCP scopes confirmed; SIEM visibility validated across infrastructure VLANs |
| 2026-01-29 | Inter-VLAN policy enforcement validation         | pfSense, Cisco switch     | Firewall rules reviewed per VLAN; unauthorized lateral movement blocked; permitted management and logging paths verified |
| 2026-01-26 | L3 routing and DHCP moved to pfSense              | pfSense, Cisco switch     | VLAN interfaces created on pfSense; DHCP pools enabled; firewall rules applied; trunk and access ports verified; SIEM and Velop clients tested for correct connectivity and IP assignment |
| 2026-01-22 | USB console cable replaced                       | Cisco switch              | FT232-based USB→RJ45 cable tested for FTDI compatibility; used for VLAN configuration; console sessions stable and responsive |
| 2026-01-19 | Console access and pre-change validation         | Cisco switch              | Verified USB console access, IOS version, licensing, VLANs, and interface usage; session lag observed during extended activity |
| 2026-01-19 | VLAN 30 creation and port assignment             | Cisco switch              | VLAN 30 (Printers) created; Gi0/7 and Gi0/8 assigned; verified using `show vlan brief` and `show interfaces status`; console lag noted prior to cable replacement |

> Notes:
> - This table represents the authoritative operational history of the environment.
> - Milestone entries establish clear baselines for future changes.
> - Chronological ordering highlights architectural progression and issue resolution.

---

## Summary

- Change management captures both incremental work and major architectural milestones.
- The final VLAN deployment establishes a stable, documented baseline.
- All future changes will be measured against this baseline to preserve clarity, control, and traceability.

---
