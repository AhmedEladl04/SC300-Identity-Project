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

<!-- SCREENSHOT: catalog overview -->
<!-- SCREENSHOT: catalog resources -->

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

<!-- SCREENSHOT: access package Review + create summary -->

## 3. Validation

### Before the request

- Signed in as **Lisa HR** at `myapplications.microsoft.com`. The `LAB-App-Internal` tile was not visible.

<!-- SCREENSHOT: My Apps without the tile -->

### Request and approval

1. As Lisa HR, opened `myaccess.microsoft.com → Access packages`, requested `AP-Engineering-Access`, and entered a justification.
2. The request showed **Pending approval**.
3. As the Global Administrator, opened **My Access → Approvals** and approved the request with a justification.

<!-- SCREENSHOT: pending request -->
<!-- SCREENSHOT: approval -->

### Result of the assignment

- Lisa HR appeared in `SG-Engineering-Team → Members`.
- The `LAB-App-Internal` tile became visible in My Apps.
- The assignment showed an expiry date 7 days from approval.

<!-- SCREENSHOT: group members -->
<!-- SCREENSHOT: My Apps showing the tile -->
<!-- SCREENSHOT: assignment with expiry -->

### Removal

1. Removed the assignment under **Access package → Assignments**, which simulates expiry.
2. Lisa HR was removed from `SG-Engineering-Team` and the tile disappeared.

<!-- SCREENSHOT: assignment removed and group membership after removal -->

### Audit trail

- Reviewed **Entra ID → Monitoring → Audit logs** (category: Entitlement Management) and confirmed events for the request, approval, assignment, and removal.

<!-- SCREENSHOT: audit log entries -->

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
