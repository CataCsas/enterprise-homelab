# VLAN Design

This document defines the VLAN structure used in the **enterprise-homelab** environment. VLANs are organized by **device role, trust level, and operational function**, supporting phased lab expansion and clear separation of concerns.

---

## VLAN Overview

| VLAN ID | Name         | Purpose |
|--------:|--------------|---------|
| 10      | Mgmt         | Network and infrastructure management |
| 20      | Security     | Security monitoring and analysis systems |
| 30      | Printers     | Network-connected printers |
| 40      | IoT          | Internet-of-Things devices (pre-secured, inactive) |
| 50      | Users_Trust  | Trusted user endpoints |
| 60      | Guest        | Guest and internet-only access (pre-secured, inactive) |

> VLANs are enforced on the Cisco switch; routing, DHCP, and policy enforcement are managed centrally by pfSense.

---

## VLAN Definitions

### VLAN 10 – Mgmt
**Purpose:** Isolated access to network and infrastructure management interfaces.  
**Devices:** Netgate SG-2100, Cisco Catalyst 3560CX, restricted administrative endpoints.  
**Notes:** No general user traffic; access tightly controlled.

### VLAN 20 – Security
**Purpose:** Security monitoring and analysis.  
**Devices:** Wazuh SIEM host, future security tooling.  
**Notes:** Receives telemetry from other VLANs; isolated from Guest and IoT networks.

### VLAN 30 – Printers
**Purpose:** Segregates network printers from other segments.  
**Devices:** Brother HL-2280DW, Brother HL-3170CDW.  
**Notes:** Access only from authorized VLANs; outbound restricted; policy enforced via ACLs and firewall.

### VLAN 40 – IoT
**Purpose:** IoT and embedded devices with limited trust.  
**Devices:** Cameras, media streaming, consumer IoT appliances.  
**Notes:** Pre-secured, currently inactive; internet access and lateral movement tightly restricted.

### VLAN 50 – Users_Trust
**Purpose:** Primary VLAN for trusted user endpoints.  
**Devices:** Laptops, mobile devices, tablets, e-readers.  
**Notes:** Wired and wireless users temporarily consolidated; future AP deployment will restore full segmentation.

### VLAN 60 – Guest
**Purpose:** Isolated internet-only access for visitors.  
**Devices:** Guest laptops, mobile devices.  
**Notes:** Pre-secured; no internal network access; activation pending dedicated guest wireless.

---

## Inter-VLAN Considerations

- Access between VLANs is **explicit and controlled**.  
- Cisco enforces VLAN boundaries with ACLs; pfSense provides routing and gateway services.  
- Monitoring and firewall policy are documented separately to maintain operational clarity.

---

## Summary

The VLAN design emphasizes:

- **Role-based segmentation**: Each VLAN aligns with a specific operational purpose.  
- **Trust-aware isolation**: High-trust, restricted, and untrusted zones are clearly separated.  
- **Phased expansion**: Dormant VLANs enable future IoT and guest segmentation without disrupting current operations.  
- **Operational clarity**: Definitions focus on function and trust rather than repeating routing or firewall mechanics.

This approach provides a **foundational structure** for incremental security, monitoring, and user segmentation within the lab environment.

---
