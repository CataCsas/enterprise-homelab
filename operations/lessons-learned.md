# Lessons Learned

This document summarizes key insights and takeaways from the design, deployment, and management of the **enterprise-homelab** environment.

---

## Key Insights

- **Planning first**: Documenting design decisions before implementation ensured consistent VLAN segmentation, IP addressing, and device configuration.  
- **Segmentation matters**: VLAN-based isolation simplified troubleshooting, improved visibility, and supported a structured network.  
- **Centralized monitoring**: Deploying Wazuh on a dedicated Linux Mint XFCE host provided reliable log collection and visibility into critical devices.  
- **Device hardening**: Closing unused services and restricting access on printers and other endpoints enhanced security and reduced attack surface.  
- **Change management**: Structured tracking of lab changes minimized misconfigurations and ensured repeatability.  

---

## Areas for Future Improvement

- **Wireless segmentation**: Upgrade to VLAN-aware APs (e.g., TP-Link EAP610) to separate IoT and trusted user devices.  
- **Expanded monitoring**: Incorporate IoT devices and additional endpoints into the SIEM once VLAN separation is implemented.  
- **Additional infrastructure**: Deploy a mini PC running Windows Server 2019 for Active Directory hands-on experience.  
- **NAS integration**: Add storage solutions with appropriate VLAN placement and access controls.  
- **Logging refinement**: Tune alerts, log retention, and reporting within Wazuh as the lab grows.  

---

## Summary

- Lessons learned will guide future expansions and lab refinements.  
- Following structured processes ensures the lab remains secure and scalable.

---
