# Change Management

This document defines the process for planning, implementing, and tracking changes within the **enterprise-homelab** environment. It serves as the authoritative record to ensure all modifications are documented, verified, and traceable.

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
   - Back up existing configurations where applicable.
   - Document the current state and intended changes in repository files.

2. **Execution**
   - Apply changes during low-activity periods where feasible.
   - Use device management interfaces appropriate to each platform.

3. **Verification**
   - Confirm connectivity and VLAN segmentation.
   - Validate device functionality and monitoring visibility.

4. **Documentation**
   - Record each completed change with:
     - Description
     - Date and rationale
     - Outcome and verification notes

---

## Change Tracking

| Date       | Change Description                                           | Affected Components            | Outcome |
|------------|-------------------------------------------------------------|--------------------------------|---------|
| 2026-02-12 | Core infrastructure stabilization and SIEM final placement  | pfSense, Cisco switch, SIEM    | Static IPs assigned; SIEM relocated; wired VLAN baseline completed; firewall rules validated; monitoring confirmed |
| 2026-02-03 | Final VLAN deployment and baseline validation               | pfSense, Cisco switch, SIEM    | All VLANs operational; inter-VLAN routing validated; DHCP and trunk/access ports confirmed; monitoring verified |
| 2026-01-29 | Inter-VLAN policy enforcement validation                    | pfSense, Cisco switch          | Firewall rules reviewed; unauthorized lateral movement blocked; permitted management/logging paths verified |
| 2026-01-26 | L3 routing and DHCP moved to pfSense                        | pfSense, Cisco switch          | VLAN interfaces and DHCP pools enabled; firewall rules applied; connectivity tested |
| 2026-01-22 | USB console cable replaced                                  | Cisco switch                   | Console access stabilized; used for VLAN configuration |
| 2026-01-19 | Console access and pre-change validation                    | Cisco switch                   | Verified console functionality, IOS version, licensing, and VLAN readiness |
| 2026-01-19 | VLAN 30 creation and port assignment                        | Cisco switch                   | VLAN 30 created; ports assigned; verification commands executed |

> Notes:
> - Table represents the authoritative operational history of the environment.
> - Milestone entries establish baselines for future changes.
> - Chronological ordering highlights architectural progression.

---

## Summary

- Change management captures incremental work and architectural milestones.
- The February 12, 2026 milestone establishes a stabilized infrastructure baseline.
- All subsequent detection engineering, monitoring expansion, and wireless segmentation changes will be evaluated against this baseline.
- Operational discipline is maintained by verification and documentation of each change.

---
