# Lessons Learned

This document summarizes key insights and takeaways from the design, deployment, and ongoing management of the **enterprise-homelab** environment.

---

## Key Insights

- **Planning before implementation**  
  Documenting design decisions in advance resulted in consistent VLAN segmentation, IP addressing, and device configuration.

- **Segmentation improves control**  
  VLAN-based isolation simplified troubleshooting, reduced unintended access, and enabled clear, enforceable trust boundaries.

- **Centralized routing and enforcement**  
  Moving inter-VLAN routing and DHCP to pfSense improved visibility, reduced configuration complexity, and aligned the lab with common enterprise designs.

- **Centralized monitoring is effective**  
  Deploying Wazuh on a dedicated Linux Mint XFCE host provided reliable log collection, analysis, and alerting for critical infrastructure.

- **Endpoint and device hardening matters**  
  Restricting access and disabling unnecessary services on printers and endpoints reduced attack surface and limited lateral movement risk.

- **Endpoint VLAN troubleshooting**  
  During VLAN50 validation, an endpoint initially failed to obtain DHCP. Layer 2 troubleshooting, including MAC table inspection, port isolation, and device swapping, identified the issue as NIC offloading and VLAN features rather than switch or firewall misconfiguration. Disabling offloading and ensuring unmanaged VLAN settings restored predictable behavior.  
  *Key takeaway: endpoint NIC behavior can interfere with VLAN-based networks, requiring validation at both endpoint and network levels.*

- **Change management reduces risk**  
  Tracking configuration changes, hardware updates, and network modifications minimized misconfigurations and improved repeatability.

- **Operational tooling impacts reliability**  
  Replacing an incompatible console cable with an FT232-based USB-to-RJ45 adapter eliminated session lag and improved day-to-day operational efficiency.

- **Troubleshooting under restrictive policies**  
  During a recent SIEM connectivity issue in VLAN20, DNS and NTP traffic was blocked due to a removed intra-VLAN rule. Resolution required explicitly adding a dedicated **VLAN20 → pfSense DNS & NTP** firewall rule, restoring update and internet access while maintaining segmentation.  
  *This demonstrates operational awareness, SOC-style troubleshooting, and controlled policy adjustments.*

---

## Areas for Future Improvement

- **Wireless segmentation**  
  Deploy VLAN-aware access points (e.g., TP-Link EAP610) to separate IoT, user, and guest wireless traffic.

- **Expanded monitoring coverage**  
  Extend SIEM ingestion to IoT devices and additional endpoints once segmentation is fully implemented.

- **Additional infrastructure**  
  Introduce a Windows Server host to support Active Directory and identity-focused lab scenarios.

- **Storage integration**  
  Add a NAS with defined VLAN placement and controlled access paths.

- **Logging refinement**  
  Continue tuning Wazuh alerting, retention, and reporting as the environment grows.

---

## Summary

- Lessons learned directly inform future design and operational decisions.
- Emphasis on planning, segmentation, centralized enforcement, and documentation supports a stable and scalable lab.
- The environment continues to evolve using the same disciplined, enterprise-aligned approach.
- Real-world operational incidents, like the VLAN20 SIEM connectivity issue, highlight the importance of careful firewall policy management.

---
