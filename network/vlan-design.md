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

> Notes: VLANs exist on the Cisco switch to **enforce segmentation and isolate traffic**. Inter-VLAN routing and DHCP are handled centrally by pfSense.

---

## VLAN Definitions

### VLAN 10 – Mgmt

**Purpose:**  
Provides isolated access to network infrastructure management interfaces.

**Typical devices:**
- Netgate SG-2100 (management interface)
- Cisco Catalyst 3560CX (L2 enforcement and monitoring connectivity)
- Administrative endpoints (as needed)

**Notes:**
- No general user traffic allowed
- Restricted access by design
- ACLs applied to control internal access

---

### VLAN 20 – Security

**Purpose:**  
Hosts security monitoring and analysis systems.

**Typical devices:**
- Linux-based SIEM host
- Future security tooling or analysis systems

**Notes:**
- Receives logs and telemetry from other VLANs
- Isolated from Guest and IoT VLANs
- pfSense provides routing and default gateway

---

### VLAN 30 – Printers

**Purpose:**  
Isolates network printers from user and management segments.

**Typical devices:**
- Brother HL-2280DW
- Brother HL-3170CDW

**Notes:**
- Accessible from selected VLANs based on operational needs
- No outbound access beyond required services
- ACLs on the switch enforce allowed communication

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
- Internet access controlled by pfSense firewall
- ACLs applied on the switch for internal segmentation

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
- Future separation planned with VLAN-aware wireless APs
- pfSense provides DHCP and default gateway

---

### VLAN 60 – Guest

**Purpose:**  
Provides isolated, internet-only access for guest devices.

**Typical devices:**
- Visitor laptops and phones

**Notes:**
- No access to internal VLANs
- Strictly controlled routing and firewall policies via pfSense
- ACLs on switch prevent unauthorized east-west traffic

---

## Inter-VLAN Considerations

- **Routing and default gateways are handled by pfSense**.  
- Cisco switch enforces VLAN segregation and ACL-based policy control.  
- Access between VLANs is explicitly controlled and monitored.  

> Notes: Detailed access policies are documented separately in firewall rules and SIEM monitoring scope.

---
