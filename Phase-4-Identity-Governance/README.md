# Phase 4 - Identity Governance

## Objective

Govern access in Microsoft Entra ID: replace standing privilege with just-in-time access, recertify access with reviews, give users time-limited access through access packages, and require acceptance of terms before access.

## Phase Structure

| # | Topic | Status |
|---|---|---|
| 01 | [Privileged Identity Management (PIM)](01-PIM.md) | ✅ Completed |
| 02 | [Access Reviews](02-Access-Reviews.md) | ✅ Completed |
| 03 | [Entitlement Management](03-Entitlement-Management.md) | ✅ Completed |
| 04 | [Terms of Use](04-Terms-of-Use.md) | ✅ Completed |

---

## 01 - Privileged Identity Management

Implemented:

- Converted Mohamed Dev's permanent **Application Developer** assignment to **eligible**
- Role settings: 2-hour maximum activation, justification and approval required
- Activation request, approval, and use of the role

Validated:

- Eligible alone did not grant access (app registration was blocked)
- After approval the role worked, then expired automatically
- Audit history recorded the assignment, request, and approval

### Result

✅ Permanent role converted to just-in-time access with approval and a full audit trail.

---

## 02 - Access Reviews

Implemented:

- **Guest review** of `SG-External-Auditors` (guest users only)
- **Role review** of Application Developer in PIM (active and eligible)
- **Self-review** of `SG-SOC-Team` by its members

Validated:

- Denying the guest removed group membership but kept the guest account
- Approving Mohamed left his assignment unchanged
- In the self-review, one user approved, one denied (and was removed), and one did not respond (no change)

### Result

✅ Guest, role, and internal group reviews completed with decisions applied and verified.

---

## 03 - Entitlement Management

Implemented:

- Catalog `Cat-Lab-Governance` containing `SG-Engineering-Team`
- Access package `AP-Engineering-Access` with approval, justification, and a 7-day expiry

Validated:

- Lisa HR requested the package and the administrator approved it
- She became a member of `SG-Engineering-Team` and gained `LAB-App-Internal` (blocked in Phase 3, Lab 2)
- Removing the assignment removed her access; the audit log recorded each step

### Result

✅ Time-limited, approved access delivered and removed through an access package.

---

## 04 - Terms of Use

Implemented:

- Terms of use (`TOU-Lab-AUP`) from a PDF policy
- Conditional Access policy requiring acceptance, tested in report-only mode first

Validated:

- The terms appeared at sign-in and were accepted by Lisa HR
- The acceptance report and sign-in logs recorded the result
- A second sign-in did not repeat the prompt

### Result

✅ Terms of use enforced with Conditional Access and verified.

---

## Not Implemented in This Phase

| Topic | What it is | Why it wasn't implemented |
|---|---|---|
| **Guest governance scenarios** (guest access packages, inactive-guest reviews) | Governance features applied to guest users | Require the tenant to be linked to an Azure subscription for guest billing, which was not done in this lab |
| **Lifecycle Workflows** | Joiner, mover, and leaver automation | Requires the Microsoft Entra ID Governance license, which the lab tenant does not have |
| **PIM for Groups and Azure resource roles** | Just-in-time access to groups and Azure resources | Outside the scope of this lab |

## Lab Limitations

- The lab tenant has a single Entra ID P2 license, assigned to the administrator. Test users were unlicensed, which is not representative of production, where each user who requests, approves, or reviews governed access needs a license.

---

## Key Concepts Demonstrated

- **Eligible vs. active** assignments and **just-in-time** access
- **Time-bound** access that expires automatically
- **Recertification:** reviewers can be selected users, owners, managers, or the members themselves
- A **denial** removes access, while an **approval** changes nothing
- **Catalogs, access packages, policies, and assignments** in entitlement management
- **Conditional Access** as the enforcement point for terms of use
- **Audit logs** as evidence for every governance action

## Phase 4 Skills Practiced

- Privileged Identity Management
- Role settings, activation, and approval
- Access reviews for groups and roles
- Self-review and review decisions
- Entitlement management
- Access packages and approval policies
- Terms of use
- Conditional Access and report-only mode
- Audit and sign-in log review

## Phase 4 Completion

Status: ✅ COMPLETE

This phase provided hands-on experience governing privileged and standard access in Microsoft Entra ID using a dedicated lab environment.



