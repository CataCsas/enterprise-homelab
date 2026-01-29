# Lessons Learned

This document summarizes key insights and takeaways from the design, deployment, and management of the **enterprise-homlab** environment.

---

## Key Insights

- **Planning first**: Documenting design decisions prior to implementation ensured consistent VLAN segmentation, IP addressing, and device configuration.  
- **Segmentation matters**: VLAN-based isolation simplified troubleshooting, improved visibility, and supported structured network policies.  
- **Centralized monitoring**: Deploying Wazuh on a dedicated Linux Mint XFCE host provided reliable log collection, analysis, and alerting for critical devices.  
- **Device hardening**: Restricting access and disabling unnecessary services on printers and endpoints reduced attack surface.  
- **Change management**: Structured tracking of lab changes, including hardware updates and network modifications, minimized misconfigurations and ensured repeatability.  
- **Hardware matters**: Choosing compatible console hardware (FT232-based USB→RJ45 cable) eliminated session lag and improved operational efficiency.  
- **Flexible architecture**: Moving inter-VLAN routing and DHCP to pfSense simplified management, increased visibility, and aligned the lab with enterprise-style practices.  

---

## Areas for Future Improvement

- **Wireless segmentation**: Deploy VLAN-aware APs (e.g., TP-Link EAP610) to separate IoT, user, and guest devices.  
- **Expanded monitoring**: Incorporate IoT devices and additional endpoints into the SIEM once segmentation is fully implemented.  
- **Additional infrastructure**: Introduce a Windows Server 2019 mini PC for hands-on Active Directory experience.  
- **NAS integration**: Add storage solutions with proper VLAN placement and access controls.  
- **Logging refinement**: Tune Wazuh alerts, retention policies, and reporting as the lab grows.  

---

## Summary

- Lessons learned provide actionable guidance for lab evolution and expansion.  
- Maintaining structured planning, monitoring, and change processes ensures the lab remains secure, scalable, and professional.

---
