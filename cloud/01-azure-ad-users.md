# Lab 01 – Microsoft Entra ID: User Creation and RBAC

## Objective
Create 2–3 Microsoft Entra ID users, assign roles simulating least-privilege access, and understand role implications in an enterprise environment. Document reasoning, assignments, and observations.

---

## Users Created

| Name        | User Type | Username                          | Role Assigned       | Privilege Scope | MFA Enforced |
|------------|-----------|----------------------------------|------------------|----------------|--------------|
| Lucy Admin | Member    | lucyadmin@labtenant.onmicrosoft.com | User Administrator | Directory      | Yes          |
| Ricky Security | Member | rickysecurity@labtenant.onmicrosoft.com | Security Operator | Directory      | Yes          |
| Bob Auditor | Guest    | bobauditor@labtenant.onmicrosoft.com | Directory Reader  | Directory      | Yes          |

*Note: MFA appears enforced at tenant-level via Security Defaults.*

---

## Steps Taken

1. Navigated to **Microsoft Entra admin center → Users → New user → Create user**.
2. Created three users to simulate **different roles in an enterprise environment**:
   - **Lucy Admin**: User Administrator — can manage other users and roles. Chosen to represent internal administrative access with directory-wide responsibilities.
   - **Ricky Security**: Security Operator — can monitor security events but cannot modify users. Chosen to show **separation of duties** between administration and security monitoring.
   - **Bob Auditor**: Directory Reader / Guest — simulates an **external auditor or contractor** with read-only access.
3. Populated identity properties minimally:
   - First Name, User Type (Member or Guest), Job Title
   - Avoided optional fields to keep accounts realistic but not fictitious.
4. Assigned roles based on **least-privilege principle**:
   - Avoided Global Administrator or other high-risk roles for safety.
   - Verified each role’s capabilities and scope before assignment.
5. Reviewed tenant-level **Security Defaults**:
   - Noted that MFA is enforced at tenant level; individual users show disabled in MFA panel, but authentication methods policies still enforce MFA.
6. Verified user creation and role assignments:
   - Confirmed that Lucy can manage users, Ricky can view security events, and Bob can only read directory information.
7. Documented all steps and rationale for GitHub portfolio.

---

## Observations & Lessons Learned

- Microsoft Entra ID roles offer **granular control**, allowing you to simulate realistic enterprise IAM practices.
- Security Defaults enforce MFA even when per-user MFA is disabled — tenant-level policies override individual settings.
- Guest users provide a safe way to simulate external access without granting full directory privileges.
- Documenting role rationale makes the exercise **portfolio-ready**, showing understanding of IAM principles, risk awareness, and operational discipline.

---

## Screenshots

| User        | Screenshot |
|------------|------------|
| Lucy Admin | ![Lucy Admin](docs/assets/cloud/lab01-Lucy-review.png) |
| Ricky Security | ![Ricky Security](docs/assets/cloud/lab01-Ricky-review.png) |
| Bob Auditor | ![Bob Auditor](docs/assets/cloud/lab01-Bob-review.png) |

> Screenshots are blurred where necessary to protect sensitive information.

---

## Notes

- Kept accounts simple to focus on **role understanding and least-privilege practice**.
- Group assignments and administrative units were skipped for this lab; will explore in subsequent exercises.
- Workflow demonstrates **hands-on identity management, validation, and reasoning**, which is critical for enterprise cloud security exercises.

---
