# Wireless Network

This document outlines the wireless network design for the **enterprise-homelab** environment, covering the current temporary deployment and the planned enterprise-style upgrade.

---

## Current Wireless Deployment

- A **Velop mesh system** provides temporary wireless coverage.
- The Velop operates in **bridge mode** with no routing, NAT, or DHCP.
- All wireless endpoints currently reside in **VLAN 50 – Users_Trust**.
- IP addressing and default gateway services are provided by **pfSense**.
- The Cisco switch enforces VLAN boundaries and internal policy controls.

**Current characteristics:**
- Wireless traffic enters the network at Layer 2
- No wireless VLAN separation is possible with the current access points
- Consolidation reflects hardware limitations, not design intent

---

## Defined but Inactive Wireless VLANs

The following VLANs are fully defined and secured at the firewall and switch layers but are **not yet active for wireless use**:

- **VLAN 40 – IoT**
- **VLAN 60 – Guest**

These VLANs remain blocked until VLAN-aware wireless access points are deployed, ensuring that enabling wireless segmentation later does not introduce risk.

---

## Planned Wireless Upgrade

- **TP-Link EAP610** access points will replace the Velop mesh.
- VLAN-aware SSIDs will map wireless traffic to dedicated VLANs:
  - **VLAN 40 – IoT**
  - **VLAN 50 – Users_Trust**
  - **VLAN 60 – Guest**
- pfSense will continue to provide DHCP, routing, and firewall enforcement.
- The Cisco switch will enforce VLAN separation and internal access control.

This upgrade enables proper isolation of wireless devices based on trust level and operational role.

---

## Wireless Security and Policy Considerations

- Wireless security relies on **VLAN-based segmentation**, not SSID trust.
- Inter-VLAN access is controlled exclusively by pfSense firewall rules.
- Switch ACLs provide supplemental internal enforcement where appropriate.
- Monitoring and logging scope will expand as VLAN-separated wireless traffic is activated.

---

## Summary

- Current wireless access is provided via a bridged consumer mesh.
- All wireless clients temporarily reside in **VLAN 50 – Users_Trust**.
- IoT and Guest VLANs are defined, secured, and intentionally inactive.
- Enterprise-grade access points will enable VLAN-aware wireless segmentation.
- The design aligns with centralized routing, firewall-first enforcement, and SOC-style visibility.

---
