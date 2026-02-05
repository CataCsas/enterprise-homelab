# Logging Scope

This document defines the scope of log collection and monitoring for the **enterprise-homelab** SIEM deployment. It documents which systems generate logs, which VLANs are covered, and the rationale behind selective visibility.

The logging strategy prioritizes **control-plane visibility, segmentation enforcement, and security-relevant events** over exhaustive endpoint logging.

---

## Monitored Devices and Systems

| Device / System           | VLAN      | Log Type / Purpose |
|---------------------------|-----------|-------------------|
| Linux SIEM Host           | Security  | Central aggregation, host monitoring, alerting |
| Netgate SG-2100 (pfSense) | Mgmt      | Firewall events, inter-VLAN policy enforcement, routing decisions |
| Cisco Catalyst 3560CX     | Mgmt      | VLAN enforcement, ACL activity, switch operational events |
| Network Printers          | Printers  | Basic operational and status events |

**Notes:**
- All logs are forwarded to the SIEM host in **VLAN 20 – Security**.
- Cisco switch logging focuses on **segmentation and access control**, not routing.
- SNMP is currently disabled on printers; logging is minimal and scoped.

---

## VLAN Coverage

- **VLAN 10 – Mgmt**  
  Firewall and switch control-plane activity, management access events.

- **VLAN 20 – Security**  
  SIEM host logs, security tooling activity, and log ingestion validation.

- **VLAN 30 – Printers**  
  Limited operational visibility to confirm availability and policy compliance.

- **VLAN 40 – IoT**  
  Defined and secured, but **not active**. No log sources currently present.

- **VLAN 50 – Users_Trust**  
  No endpoint-level monitoring. Visibility limited to:
  - Firewall allow/deny events
  - DHCP activity
  - Policy violations or anomalies

- **VLAN 60 – Guest**  
  Defined and secured, but **not active**. No endpoint monitoring planned beyond firewall enforcement once enabled.

**Notes:**
- VLAN scope reflects **trust boundaries and operational relevance**.
- User and guest privacy is preserved by avoiding deep endpoint inspection.

---

## Log Types and Collection Strategy

- **Syslog** is used for network infrastructure where supported.
- **Host-based logging** applies only to the SIEM system itself.
- Firewall rule logging is **explicit and selective**, not default-enabled.
- No reliance on implicit or blanket logging for security-critical paths.

**Design intent:**
- Preserve pfSense and SIEM performance
- Maintain high signal-to-noise ratio
- Make policy intent auditable through explicit rules

---

## Scope Control and Evolution

- Logging scope is intentionally conservative.
- Additional sources will be added only when they provide:
  - Clear security value
  - Actionable signals
  - Minimal operational overhead

Expansion targets include:
- IoT VLAN telemetry after wireless segmentation
- Validation of east–west traffic enforcement
- IDS/IPS integration once traffic baselines are established

---

## Summary

- Logging focuses on **infrastructure, segmentation, and policy enforcement**.
- User and guest devices are not deeply monitored.
- IoT and Guest VLANs are pre-secured and currently inactive.
- Visibility is expanded deliberately to avoid noise and misinterpretation.

---
