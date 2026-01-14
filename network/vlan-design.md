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

---

## VLAN Definitions

### VLAN 10 – Mgmt

**Purpose:**  
Provides isolated access to network infrastructure management interfaces.

**Typical devices:**
- Netgate SG-2100 (management interface)
- Cisco Catalyst 3560CX (management SVI)
- Administrative access endpoints (when required)

**Notes:**
- Not used for general user traffic
- Restricted access by design

---

### VLAN 20 – Security

**Purpose:**  
Hosts security monitoring and analysis systems.

**Typical devices:**
- Linux-based SIEM host
- Future security tooling or analysis systems

**Notes:**
- Receives logs and telemetry from other VLANs
- No direct exposure to guest or IoT networks

---

### VLAN 30 – Printers

**Purpose:**  
Isolates network printers from user and management segments.

**Typical devices:**
- Brother HL-2280DW
- Brother HL-3170CDW

**Notes:**
- Access permitted from selected internal VLANs as required
- No outbound access beyond required services

---

### VLAN 40 – IoT

**Purpose:**  
Contains IoT and embedded devices with limited trust.

**Typical devices:**
- Cameras
- Media streaming devices
- Consumer IoT appliances

**Notes:**
- Restricted east-west communication
- Internet access constrained by policy

---

### VLAN 50 – Users_Trust

**Purpose:**  
Primary VLAN for trusted user endpoints.

**Typical devices:**
- Personal laptops
- Mobile devices
- Tablets and e-readers

**Notes:**
- Temporary consolidation of wireless endpoints
- Future separation planned once VLAN-aware wireless infrastructure is deployed

---

### VLAN 60 – Guest

**Purpose:**  
Provides isolated, internet-only access for guest devices.

**Typical devices:**
- Visitor laptops and phones

**Notes:**
- No access to internal VLANs
- Strictly controlled routing and firewall policies

---

## Inter-VLAN Considerations

- Inter-VLAN routing is performed at the Layer 3 switch
- Default gateway for each VLAN is provided by an SVI
- Access between VLANs is explicitly controlled

Detailed access policies are defined outside the scope of this document.

---
