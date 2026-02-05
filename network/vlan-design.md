# VLAN Design

This document defines the VLAN structure used in the **enterprise-homelab** environment. VLANs are assigned based on **device role, trust level, and operational function**.

The design prioritizes clear separation between management, security infrastructure, user endpoints, and untrusted devices.

---

## VLAN Overview

| VLAN ID | Name         | Purpose |
|--------:|--------------|---------|
| 10      | Mgmt         | Network and infrastructure management |
| 20      | Security     | Security monitoring and analysis systems |
| 30      | Printers     | Network-connected printers |
| 40      | IoT          | Internet-of-Things devices |
| 50      | Users_Trust  | Trusted user endpoints |
| 60      | Guest        | Guest and internet-only access |

> VLANs are defined on the Cisco switch to **enforce segmentation and isolate traffic**. Inter-VLAN routing and DHCP are handled centrally by pfSense.

---

## VLAN Definitions

### VLAN 10 – Mgmt

**Purpose:**  
Provides isolated access to network infrastructure management interfaces.

**Typical devices:**
- Netgate SG-2100 (management interface)
- Cisco Catalyst 3560CX
- Administrative endpoints (restricted)

**Notes:**
- No general user traffic permitted
- Access tightly controlled
- Internal access governed by firewall rules and switch ACLs

---

### VLAN 20 – Security

**Purpose:**  
Hosts security monitoring and analysis systems.

**Typical devices:**
- Linux-based SIEM host
- Future security tooling

**Notes:**
- Receives logs and telemetry from other VLANs
- Isolated from Guest and IoT networks
- Routing and default gateway provided by pfSense

---

### VLAN 30 – Printers

**Purpose:**  
Isolates network printers from user and management segments.

**Typical devices:**
- Brother HL-2280DW
- Brother HL-3170CDW

**Notes:**
- Access permitted only from explicitly authorized VLANs
- Outbound access restricted to required services
- Policy enforced via firewall rules and switch ACLs

---

### VLAN 40 – IoT

**Purpose:**  
Contains IoT and embedded devices with limited trust.

**Typical devices:**
- Cameras
- Media streaming devices
- Consumer IoT appliances

**Notes:**
- VLAN is defined and secured
- Currently inactive pending VLAN-aware wireless deployment
- Internet access and lateral movement tightly restricted by design

---

### VLAN 50 – Users_Trust

**Purpose:**  
Primary VLAN for trusted user endpoints.

**Typical devices:**
- Personal laptops
- Mobile devices
- Tablets and e-readers

**Notes:**
- Wired and wireless user endpoints currently reside here
- Wireless consolidation reflects access point limitations, not design intent
- Full separation planned with enterprise-grade VLAN-aware APs

---

### VLAN 60 – Guest

**Purpose:**  
Provides isolated, internet-only access for guest devices.

**Typical devices:**
- Visitor laptops and mobile devices

**Notes:**
- VLAN is defined and pre-secured
- No access to internal networks
- Activated only when dedicated guest wireless is deployed

---

## Inter-VLAN Considerations

- **pfSense performs all inter-VLAN routing and gateway services**
- Cisco switch enforces VLAN boundaries and supplemental ACLs
- All inter-VLAN access is explicit, controlled, and logged where applicable

> Detailed firewall policies and monitoring scope are documented separately.

---
