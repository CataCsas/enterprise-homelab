# IP Addressing

This document defines the IP addressing approach for the **enterprise-homelab** environment. It focuses on VLAN segmentation, static vs. dynamic assignments, and centralized DHCP management.

---

## Addressing Principles

- **Static IPs** are reserved for critical infrastructure and administrative devices:
  - Edge firewall / gateway
  - Core switch
  - Security monitoring host (SIEM)
  - Network printers
- **DHCP** is used for general user devices, IoT devices, and guest endpoints.
- Each VLAN has a distinct subnet to simplify management, troubleshooting, and segmentation.
- VLAN40 (IoT) and VLAN60 (Guest) are pre-secured and inactive, ready for future WiFi segmentation.
- Documented addressing ensures reproducibility, visibility, and professional operational standards.

---

## VLAN Addressing Overview

| VLAN ID | Name         | Purpose |
|--------:|--------------|---------|
| 10      | Mgmt         | Management and core infrastructure |
| 20      | Security     | Security monitoring hosts and tools |
| 30      | Printers     | Network printers |
| 40      | IoT          | IoT and embedded devices (pre-secured, inactive) |
| 50      | Users_Trust  | Trusted user endpoints, including wireless devices |
| 60      | Guest        | Guest devices with internet-only access (pre-secured, inactive) |

---

## Static IP Assignments

Critical devices receive static IPs or DHCP reservations within their VLAN subnet, including:

- Edge firewall / gateway
- Core switch management interface
- Security monitoring host (SIEM)
- Network printers

Static assignments ensure consistent connectivity, predictable routing, and reliable logging.

---

## DHCP Management

- DHCP is centrally managed by pfSense for all VLANs.
- Each VLAN has a defined DHCP pool for dynamic client addressing.
- Key devices use DHCP reservations to maintain predictable addresses.

---

## Best Practices

- **Segmentation first**: VLANs separate device roles and trust levels.
- **Static vs. dynamic**: Reserve static IPs for infrastructure; use DHCP for general endpoints.
- **Centralized management**: pfSense handles all DHCP and routing, ensuring visibility and control.
- **Document internally**: Maintain detailed IP assignments and reservations for reproducibility and troubleshooting.

---

## Summary

- VLAN-based addressing improves clarity, security, and operational control.
- Static IPs and DHCP reservations ensure reliable connectivity for critical devices.
- Pre-secured VLANs support phased lab expansion.
- The addressing strategy supports lab growth, experimentation, and professional SOC-style operations.

---
