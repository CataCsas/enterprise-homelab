# Wireless Network

This document describes the wireless network deployment in the **enterprise-homelab**, covering the temporary setup and planned enterprise-style upgrade.

---

## Current Deployment

- **Velop mesh system** provides temporary wireless coverage.  
- Operates in **bridge mode**; Layer 2 connectivity only.  
- Wireless endpoints reside in **VLAN 50 – Users_Trust**.  
- IP addressing, DHCP, and routing are handled centrally by pfSense.  
- Cisco switch enforces VLAN boundaries for internal traffic.

**Notes:**  
- No wireless VLAN separation is currently possible.  
- Consolidation reflects hardware limitations, not design intent.

---

## Defined but Inactive Wireless VLANs

- **VLAN 40 – IoT**  
- **VLAN 60 – Guest**

> These VLANs are pre-secured at the switch and firewall layers but remain inactive until VLAN-aware APs are deployed.

---

## Planned Upgrade

- **TP-Link EAP610** access points will replace the Velop mesh.  
- VLAN-aware SSIDs will map traffic to dedicated VLANs:
  - **VLAN 40 – IoT**
  - **VLAN 50 – Users_Trust**
  - **VLAN 60 – Guest**
- Wireless traffic will maintain segregation consistent with VLAN definitions.  
- Monitoring and logging scope will extend to newly segmented wireless traffic once active.

**Notes:**  
- Wireless security relies on VLAN segmentation rather than SSID trust.  
- Inter-VLAN access and policy enforcement remain centralized.

---

## Summary

- Temporary wireless clients are consolidated in **VLAN 50 – Users_Trust**.  
- IoT and Guest VLANs are pre-secured and inactive.  
- Enterprise-grade APs will enable VLAN-aware wireless segmentation.  
- Wireless evolution supports phased expansion while preserving operational control and visibility.

---
