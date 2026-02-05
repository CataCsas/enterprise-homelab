# Threat Model

This document outlines potential security threats to the **enterprise-homelab** environment and the controls implemented to mitigate them. It reflects the current architecture and emphasizes enforceable, observable security controls.

---

## Scope

- Covers internal VLANs, critical infrastructure, and wired and wireless endpoints.
- Focuses on realistic risks within the lab environment, including misconfiguration, unauthorized access, and internet exposure.
- Emphasizes prevention and containment through segmentation and policy enforcement.
- VLAN segmentation is enforced at Layer 2 by the Cisco switch.
- Inter-VLAN access, routing, NAT, and trust boundaries are enforced by pfSense firewall policy.

---

## Identified Threats and Mitigations

| Threat                      | Affected Components            | Mitigation / Controls |
|-----------------------------|--------------------------------|-----------------------|
| Unauthorized administrative access | Mgmt VLAN, Security VLAN | Isolated management VLAN, restricted firewall rules, limited administrative endpoints |
| Misconfigured VLANs or trunking | Cisco switch, pfSense | Documented VLAN design, explicit trunk configuration, validation during change management |
| Firewall policy misconfiguration | pfSense | Default-deny policy, explicit allow rules per VLAN, change tracking and verification |
| Lateral movement between VLANs | Internal VLANs | Inter-VLAN traffic denied by default; access granted only by explicit firewall rules |
| Compromised IoT devices | IoT VLAN (future) | Dedicated VLAN, no access to management or security networks, internet access tightly scoped |
| Rogue or untrusted wireless endpoints | Users_Trust VLAN | Treated as untrusted by default; no access to management or security VLANs |
| Printer abuse or pivoting | Printers VLAN | Isolated printer VLAN, restricted inbound access, no internet access, limited protocols |
| Internet-based attacks | Edge firewall | Stateful firewalling, NAT, ingress filtering, deny-by-default inbound policy |
| SIEM host compromise | Security VLAN | Isolated VLAN, limited access paths, host monitoring, regular updates and backups |

---

## Observability and Detection Considerations

- Firewall enforcement provides visibility into:
  - Blocked inter-VLAN access attempts
  - Policy violations
  - Unexpected traffic paths
- Switch logs provide visibility into:
  - VLAN enforcement
  - Interface state and access control behavior
- The SIEM focuses on **control-plane and policy-relevant events**, not full traffic inspection.

Deep east–west traffic inspection is intentionally deferred until it provides clear operational value.

---

## Summary

- Risk is primarily mitigated through **segmentation**, **default-deny firewall policy**, and **centralized enforcement**.
- Controls reflect real enterprise practices rather than theoretical coverage.
- Threat modeling remains aligned with deployed capabilities and observable telemetry.
- Future expansions (wireless VLANs, IoT activation) inherit the same security posture by design.

---
