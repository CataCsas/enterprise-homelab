# Lab 01 – Microsoft Entra ID (Azure AD) User Creation and RBAC

## Objective

Simulate enterprise identity management by creating internal and external users in Microsoft Entra ID, assigning least-privilege roles, and validating tenant-level security defaults (MFA enforcement).

This lab demonstrates:
- User provisioning
- Role-Based Access Control (RBAC)
- Guest (external) user onboarding
- Least privilege principles
- Security defaults enforcement

---

## Environment

- Tenant: Default Directory
- Subscription: Azure Free Trial
- Identity Platform: Microsoft Entra ID (formerly Azure Active Directory)
- Security Defaults: Enabled (MFA enforced)

---

## Users Created

| Name           | User Type | Username | Role Assigned | Privilege Scope | MFA Enforced |
|---------------|-----------|----------|---------------|-----------------|--------------|
| Lucy Admin   | Member    |          |               | Directory       | Yes |
| Ricky Security | Member  |          |               | Directory       | Yes |
| Bob Auditor  | Guest     |          |               | Directory       | Yes |

> Roles were assigned according to least-privilege principles.

---

## Role Design Rationale

### Lucy Admin
- Role:
- Justification:
- Why not Global Administrator:

### Ricky Security
- Role:
- Justification:

### Bob Auditor (Guest)
- Role:
- Justification:
- Reason for Guest user type:

---

## Configuration Steps

### 1. User Creation
- Navigated to: Identity → Users → New user → Create new user
- Entered user details
- Generated temporary password

### 2. Role Assignment
- Assigned directory role during/after user creation
- Verified role assignment under:
  Identity → Roles & administrators

### 3. Guest User Invitation
- Selected "Invite external user"
- Entered placeholder external email
- Assigned read-only role

### 4. Security Defaults Verification
- Confirmed tenant-level Security Defaults enabled
- MFA enforced automatically

---

## Validation

- Verified users appear under Identity → Users
- Confirmed role membership under Identity → Roles & administrators
- Confirmed Guest user type for external account
- Confirmed Security Defaults enabled

---

## Screenshots

Stored under:
`/docs/assets/cloud/`

Suggested naming convention:
- lab01-user-review.png
- lab01-role-assignment.png
- lab01-guest-user.png
- lab01-security-defaults.png

*(Insert screenshots below with brief caption for each.)*

---

## Observations

- Notes on Entra ID interface differences vs legacy Azure AD
- Role assignment workflow behavior
- Guest user invitation process
- MFA enforcement behavior under Security Defaults

---

## Lessons Learned

- Importance of least-privilege RBAC
- Distinction between Member and Guest users
- Security Defaults simplify baseline security posture
- Administrative role scoping considerations

---
