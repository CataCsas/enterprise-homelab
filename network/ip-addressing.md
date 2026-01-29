# IP Addressing

This document defines the IP addressing approach for the **enterprise-homelab** environment. It focuses on VLAN segmentation, static vs. dynamic assignments, and centralized DHCP management.

---

## Addressing Principles

- **Static IPs** are reserved for critical infrastructure and administrative devices:
  - Edge firewall / gateway
  - Core switch
  - Security monitoring host (SIEM)
- **DHCP** is used for general user devices, IoT devices, and guest endpoints.
- Each VLAN has a distinct subnet to simplify management, troubleshooting, and segmentation.
- Documented addressing ensures reproducibility and professional operational standards.

---

## VLAN Addressing Overview

| VLAN ID | Name         | Purpose |
|--------:|--------------|---------|
| 10      | Mgmt         | Management and core infrastructure |
| 20      | Security     | Security monitoring hosts and tools |
| 30      | Printers     | Network printers |
| 40      | IoT          | IoT and embedded devices |
| 50      | Users_Trust  | Trusted user endpoints, including wireless devices |
| 60      | Guest        | Guest devices with internet-only access |

---

## Static IP Assignments

Critical devices receive static IPs within their VLAN subnet, including:

- Edge firewall / gateway
- Core switch management interface
- Security monitoring host and network printers

Static assignments ensure consistent connectivity and predictable routing within the lab.

---

## DHCP Management

- DHCP is centrally managed by pfSense for all VLANs.
- Each VLAN has a defined DHCP pool for dynamic client addressing.
- Certain devices (printers, monitoring hosts) use DHCP reservations to maintain predictable addresses.

---

## Best Practices

- **Segmentation first**: VLANs separate device roles and trust levels.
- **Static vs. dynamic**: Reserve static IPs for infrastructure; use DHCP for general endpoints.
- **Centralized management**: pfSense handles all DHCP and routing, ensuring visibility and control.
- **Document internally**: Keep detailed IP assignments and reservations in internal lab records.

---

## Summary

- VLAN-based addressing improves clarity, security, and troubleshooting.
- Static IPs are used for infrastructure and critical devices; other endpoints are dynamically assigned.
- The structure supports lab growth, experimentation, and professional practices.

---
