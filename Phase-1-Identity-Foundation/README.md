# Phase 1 — identity foundation

Hands-on Microsoft Entra ID P2 lab covering the design, administration, and governance of user identities for an SC-300 portfolio.

## Objectives

- Establish a secure tenant baseline and identity model.
- Manage users, groups, administrative units (AUs), roles, and dynamic identity features.
- Configure identity access capabilities, including licensing, devices, guest access, and cross-tenant access.

## Environment

- Microsoft Entra ID P2 tenant
- Lab tenant intentionally limited to **25 users maximum**
- Current identities: **10 internal users** and **1 external guest**

## Completed Work

| Section | Scope |
|---|---|
| 01 — Tenant Baseline | Tenant configuration and baseline review |
| 02 — Entra Roles | Role-based administration |
| 03 — Identity Model | Workforce and external identity design |
| 04 — Users, Groups & Administrative Units | User, group, and AU management |
| 05 — Dynamic Identity | Dynamic groups and custom security attributes |
| 06 — Identity Access | Licensing, device identities, guests, and cross-tenant access |
| Company Branding | Tenant branding configuration |

Validation was intentionally skipped for this phase.

## Lab Identities and Structure

- **Internal identities:** 10 lab users supporting workforce and administrative scenarios.
- **External identity:** 1 guest user, **External Auditor**, with limited directory access and no privileged Entra role.
- **Groups:** Security and role-aligned groups, including `SG-SOC-Team` for group-based licensing scenarios.
- **Administrative units:** Used to demonstrate scoped administration and delegated management.

## Key Concepts Demonstrated

- Least-privilege role assignment and scoped administration
- User, guest, group, and administrative-unit lifecycle management
- Dynamic group membership and custom security attributes
- Group-based licensing
- Microsoft Entra registered, joined, and hybrid joined device identities
- External collaboration and cross-tenant access considerations

## Evidence

Screenshots and configuration evidence are maintained alongside the relevant section documentation, covering tenant settings, roles, identity objects, group and AU configuration, dynamic identity features, identity access, and company branding.

## Outcome

Phase 1 establishes a documented Microsoft Entra identity foundation for later authentication, Conditional Access, and identity protection work in the SC-300 lab.

