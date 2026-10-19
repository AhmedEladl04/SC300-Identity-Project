# Tenant Baseline

## 1. Tenant Information

| Property                    | Value                        |
| --------------------------- | ---------------------------- |
| **Tenant Name**             | `<lab-tenant>` (redacted)    |
| **Primary Domain**          | `<lab-domain>.onmicrosoft.com` (redacted) |
| **Microsoft Entra License** | Microsoft Entra ID P2        |
| **Users**                   | 1                            |
| **Groups**                  | 0                            |
| **Applications**            | 0                            |
| **Devices**                 | 0                            |

### Initial Tenant State

The lab Microsoft Entra tenant is currently in an almost clean state, containing only the initial administrator account.

At the beginning of the project, the tenant has:

* No custom groups
* No registered or joined devices
* No application registrations
* No additional users
* No delegated administrators

This provides a clean baseline from which the SC-300 practical implementation can be built and documented.

---

## 2. Administrative Access

### Current Configuration

* **Total users:** 1
* **Global Administrators:** 1
* **Delegated administrators:** None

The current administrator account has the **Global Administrator** role and is responsible for managing the tenant.

No delegated administrative model has been implemented yet.

### Initial Assessment

The tenant currently relies entirely on a highly privileged Global Administrator account. As the project progresses, delegated administrative roles will be implemented according to the principle of **least privilege**.

The goal is to avoid using Global Administrator for routine administrative tasks when a more specific Microsoft Entra role can provide the required permissions.

---

## 3. User Settings

The following user settings are currently enabled:

* Users can create security groups.
* Users can register applications.
* Users can connect their accounts with LinkedIn.
* Users can remain signed in.

### Initial Assessment

These settings will be reviewed during the project to determine whether they are appropriate for an enterprise environment.

Particular attention will be given to:

* Application registration permissions
* Security group creation permissions
* The security implications of allowing users to remain signed in
* The business and security implications of connected social accounts

These settings will be revisited as part of the authentication, workload identity, and identity governance phases.

---

## 4. Guest Users and External Collaboration

### Current Configuration

* Guest users have limited access to directory objects.
* Only users assigned to administrative roles can invite guest users.
* External users are allowed to leave the organization.
* Guest self-service is not enabled.
* Guest invitations are allowed from any domain.
* No delegated external administrators are configured.

### Initial Assessment

The current configuration restricts guest invitations to users with appropriate administrative roles, reducing the ability of ordinary users to introduce external identities into the tenant.

However, invitations are currently permitted from any domain. This provides broad collaboration capability but may require additional restrictions depending on the organization's business requirements.

External identity controls will be further explored during the external identity and identity governance portions of the project.

---

## 5. Domain Services

No additional domain services are currently configured.

The tenant is currently using its Microsoft-provided `onmicrosoft.com` domain as the primary domain.

A custom domain may be evaluated later if required for the project, but it is not currently necessary for the practical SC-300 implementation.

---

## 6. Initial Security Assessment

The initial tenant assessment identified the following conditions:

1. The tenant currently has only one user.
2. The only administrator is a Global Administrator.
3. No delegated administrators have been configured.
4. No custom groups currently exist.
5. Users are currently allowed to create security groups.
6. Users are currently allowed to register applications.
7. Guest invitations are restricted to users with administrative roles.
8. Guest users have limited directory access.
9. Guest invitations are currently allowed from any domain.
10. No devices or application registrations currently exist.
11. No additional domain services are configured.

This baseline will be used to measure the changes introduced throughout the SC-300 practical project.

---
