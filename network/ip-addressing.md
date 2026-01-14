# IP Addressing

This document defines the IP addressing scheme for the **enterprise-homelab** environment. The goal is to assign addresses consistently, minimize conflicts, and clearly distinguish between VLANs, static devices, and DHCP clients.

---

## Addressing Principles

- **Static IPs** are assigned to critical infrastructure:
  - Edge firewall (pfSense)
  - Core switch (Cisco Catalyst 3560CX)
- **Reserved IPs** are allocated for essential devices:
  - SIEM host
  - Network printers
- **DHCP** is used for IoT devices, general user endpoints and guest devices.
- **Address ranges** are segmented per VLAN for clarity and manageability.
- IP assignments are documented to maintain reproducibility and facilitate troubleshooting.

---

## VLAN Addressing Overview

| VLAN ID | Name         | Subnet           | Notes |
|--------:|--------------|-----------------|-------|
| 10      | Mgmt         | 192.168.10.0/24 | Static IPs for firewall, switch, admin devices |
| 20      | Security     | 192.168.20.0/24 | Reserved IPs for SIEM host |
| 30      | Printers     | 192.168.30.0/24 | Reserved IPs for printers |
| 40      | IoT          | 192.168.40.0/24 | DHCP for IoT devices |
| 50      | Users_Trust  | 192.168.50.0/24 | DHCP for trusted users and temporary wireless devices |
| 60      | Guest        | 192.168.60.0/24 | DHCP for guest devices, internet-only access |

---

## Static IP Assignments

| Device                      | VLAN   | IP Address     | Purpose |
|------------------------------|--------|---------------|---------|
| Netgate SG-2100 (LAN1)       | Mgmt   | 192.168.10.1  | Gateway / firewall |
| Cisco Catalyst 3560CX (Mgmt) | Mgmt   | 192.168.10.2  | Layer 3 SVI / switch management |

> Notes:
> - Static addresses are documented to prevent conflicts.

---

## DHCP Reservations

Certain devices require predictable IP addresses. These are assigned as **reservations in DHCP**:

| Device                      | VLAN   | Reserved IP   | Purpose |
|------------------------------|--------|---------------|---------|
| Linux SIEM Notebook           | Security | 192.168.20.10 | Monitoring and log aggregation |
| Brother HL-2280DW Printer     | Printers | 192.168.30.10 | Network printing |
| Brother HL-3170CDW Printer    | Printers | 192.168.30.11 | Network printing |

---

## DHCP Considerations

- DHCP is provided by the Cisco switch.
- Each VLAN has a defined **DHCP pool** within its subnet.
- DHCP reservations are used for predictable IP assignment:
  - Printers
  - SIEM host
- General users, IoT devices, and guest devices receive dynamic addresses from their VLAN pool.

---

## Summary

- Clear segmentation per VLAN simplifies troubleshooting.
- Static addresses are reserved for infrastructure and critical endpoints.
- DHCP handles all general client devices.
- Documented addressing ensures reproducibility and clarity for future lab expansions.

---
