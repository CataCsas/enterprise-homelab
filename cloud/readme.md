# Cloud Labs

This folder contains structured Microsoft Entra ID (Azure AD) labs focused on identity management, RBAC governance, and tenant-level security hardening.

Each lab documents:
- Objective and scope
- Identity and RBAC configuration
- Administrative decision-making
- Security control implementation
- Validation through audit logs or role review
- Observations from a governance perspective

The progression follows a structured identity path:
1. Establish identity objects and role foundations  
2. Harden administrative and tenant-level controls  
3. Simulate identity lifecycle management  

---

## Current Labs

1. [01-azure-ad-users.md](01-azure-ad-users.md)  
   **User Creation & RBAC Simulation**  
   Establishes identity objects, role assignments, and baseline administrative structure.

2. [02-azure-ad-identity-hardening.md](02-azure-ad-identity-hardening.md)  
   **Tenant Identity Hardening**  
   Reviews administrative posture, introduces emergency access planning, restricts default tenant behaviors, and validates changes through audit logs.

3. *(Planned)* **Account Lifecycle Simulation**  
   Simulates joiner, mover, and leaver scenarios including role adjustments, group membership changes, and account deprovisioning validation.

---

> Each lab is documented in a single Markdown file with supporting screenshots stored under `docs/assets/cloud/`.
>  
> The objective is to demonstrate practical administrative control, measurable risk reduction, and clear documentation of cloud identity decisions.

---
