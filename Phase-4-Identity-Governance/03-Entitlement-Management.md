# 03 - Entitlement Management

## Objective

Use Microsoft Entra entitlement management to give a user time-limited access through an access package, with a request, approval, automatic expiry, and an audit trail.

## 1. Catalog

### Configuration

| Setting | Value |
|---|---|
| Name | `Cat-Lab-Governance` |
| Description | Lab catalog for governance access packages |
| Enabled | Yes |
| Enabled for external users | No |

### Implementation

1. Opened **ID Governance → Entitlement management → Catalogs → New catalog**.
2. Created `Cat-Lab-Governance`.
3. Added the group `SG-Engineering-Team` as a resource under **Resources → Add resources → Groups and Teams**.

<img width="1608" height="682" alt="Screenshot 2026-10-16 185003" src="https://github.com/user-attachments/assets/11918bef-bca9-496a-87db-8a4d82878ad0" />
<img width="1623" height="486" alt="Screenshot 2026-10-16 184958" src="https://github.com/user-attachments/assets/08cd91eb-c7aa-402c-9126-a4f19720f0ae" />

## 2. Access Package

### Configuration

| Tab | Setting |
|---|---|
| Basics | `AP-Engineering-Access`, catalog `Cat-Lab-Governance` |
| Resource roles | `SG-Engineering-Team` as **Member** |
| Requests | Users in the directory, specific users and groups: **Lisa HR**. Request type: self. Requestor justification required |
| Approval | One stage, specific approver: lab Global Administrator, decision within 14 days, approver justification required |
| Lifecycle | Access expires after **7 days**, extension not allowed |

The access package grants membership in `SG-Engineering-Team`, the group assigned to the `LAB-App-Internal` enterprise application in Phase 3, Lab 2.

<img width="1387" height="775" alt="Screenshot 2026-10-16 190025" src="https://github.com/user-attachments/assets/91540c44-fd7c-400c-8c41-77309f5f7013" />

## 3. Validation

### Before the request

- Signed in as **Lisa HR** at `myapplications.microsoft.com`. The `LAB-App-Internal` tile was not visible.

<img width="1805" height="695" alt="Screenshot 2026-10-16 190220" src="https://github.com/user-attachments/assets/7d3fbe4f-3f7e-4c92-9c9a-6acc5552b452" />

### Request and approval

1. As Lisa HR, opened `myaccess.microsoft.com → Access packages`, requested `AP-Engineering-Access`, and entered a justification.
2. The request showed **Pending approval**.
3. As the Global Administrator, opened **My Access → Approvals** and approved the request with a justification.

<img width="1610" height="401" alt="Screenshot 2026-10-16 190401" src="https://github.com/user-attachments/assets/5f4df8b0-1308-48f3-bebc-060ec251d741" />
<img width="1491" height="521" alt="Screenshot 2026-10-16 190429" src="https://github.com/user-attachments/assets/efc95c64-7cae-4fae-bea1-a21d9bcdeed8" />
<img width="1611" height="590" alt="Screenshot 2026-10-16 190451" src="https://github.com/user-attachments/assets/dbb6c578-d330-476c-8d93-1db8137fa2bb" />


### Result of the assignment

- Lisa HR appeared in `SG-Engineering-Team → Members`.
- The `LAB-App-Internal` tile became visible in My Apps.
- The assignment showed an expiry date 7 days from approval.

<img width="1362" height="587" alt="Screenshot 2026-10-16 190525" src="https://github.com/user-attachments/assets/cf252cf2-3481-48a5-a826-b73a26b1d4f8" />
<img width="1691" height="850" alt="Screenshot 2026-10-16 190804" src="https://github.com/user-attachments/assets/2cfa840e-ac83-4f0f-9b47-d40f39c5e38f" />

### Removal

1. Removed the assignment under **Access package → Assignments**, which simulates expiry.
2. Lisa HR was removed from `SG-Engineering-Team` and the tile disappeared.

<img width="930" height="642" alt="image" src="https://github.com/user-attachments/assets/4a58b435-49bd-4038-8728-0baafe890703" />

### Audit trail

- Reviewed **Entra ID → Monitoring → Audit logs** (category: Entitlement Management) and confirmed events for the request, approval, assignment, and removal.

<img width="1247" height="573" alt="Screenshot 2026-10-16 191200" src="https://github.com/user-attachments/assets/e07a381a-326b-4dea-aef4-ed16e325f23f" />

## Limitations

- **Guest scenario not implemented.** Entitlement policies that include guests, and direct assignment of guests, require the tenant to be linked to an Azure subscription for Entra ID Governance guest billing. This lab did not link a subscription, so the access package was tested with an internal user.
- **Licensing.** The lab tenant has a single Entra ID P2 license, assigned to the administrator. Test users were unlicensed, which is not representative of production, where each user who requests, approves, or reviews governed access needs a license.

## Result

✅ Access package configured with approval and expiry. A user requested access, was approved, gained the application through group membership, and lost it when the assignment was removed, with the audit trail verified.

## Key Takeaways

- A **catalog** is a container of resources (groups, applications, SharePoint sites) that access packages draw from.
- An **access package** bundles resource roles with one or more **policies**: who can request, who approves, how long access lasts, and whether it is reviewed.
- An **assignment** is a user's active grant and **expires automatically**, which stops access from accumulating.
- Requests can require **justification** and **approval**, and every step is recorded in the audit logs.
- **Connected organizations** let users from partner tenants request access themselves. Guest scenarios need a linked subscription for billing.
- Useful roles: **Identity Governance Administrator**, **Catalog owner**, **Access package manager**, and **Access package assignment manager**.
