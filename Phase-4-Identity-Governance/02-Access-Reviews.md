# 02 - Access Reviews

## Objective

Use Microsoft Entra access reviews to recertify access: a guest user in a group, a privileged role assignment, and an internal group using self-review.

## 1. Preparation

- Created the security group `SG-External-Auditors` and added the guest user **External Auditor** as a member.
- Confirmed `SG-SOC-Team` contains John SOC, Sarah SOC, and Omar SOC.

<!-- SCREENSHOT: SG-External-Auditors members (guest email blurred) -->

## 2. Guest Review

### Configuration

| Setting | Value |
|---|---|
| Resource | Group `SG-External-Auditors` |
| Scope | Guest users only |
| Reviewer | Selected user: lab Global Administrator |
| Duration / recurrence | 3 days, one time |
| Auto apply results | Enabled |
| If reviewers don't respond | No change |
| Require reason | Enabled |
| Action on denied guests | Remove user's membership from the resource |

<!-- SCREENSHOT: review settings summary -->

### Validation

1. Opened the review at `myaccess.microsoft.com → Access reviews`.
2. Selected **Deny** for External Auditor with the reason "Engagement ended".
3. Stopped the review and checked **Results**. The decision was applied.
4. Confirmed that External Auditor was removed from `SG-External-Auditors`, while the guest account still exists under **Users**.

<!-- SCREENSHOT: Deny decision -->
<!-- SCREENSHOT: results page -->
<!-- SCREENSHOT: empty group and guest account still present -->

## 3. Role Review (Privileged Identity Management)

### Configuration

| Setting | Value |
|---|---|
| Location | **PIM → Microsoft Entra roles → Access reviews** |
| Role | Application Developer |
| Assignment type | All active and eligible |
| Reviewer | Selected user: lab Global Administrator |
| Duration / recurrence | 3 days, one time |
| Auto apply results | Enabled |
| If reviewers don't respond | No change |
| Recommendations / require reason | Enabled |

Entra role reviews are created and completed in PIM, not in the main Access reviews page.

<!-- SCREENSHOT: role review settings -->

### Validation

1. Reviewed the assignment under **PIM → Review access**.
2. Approved Mohamed Dev with the reason "Still needed for development work".
3. Stopped the review. With auto apply enabled, the results were applied automatically.
4. Confirmed that Mohamed's eligible assignment was unchanged. Approving a user keeps their access.

<!-- SCREENSHOT: Approve decision -->
<!-- SCREENSHOT: results and unchanged eligible assignment -->

## 4. Internal Group Self-Review

### Configuration

| Setting | Value |
|---|---|
| Resource | Group `SG-SOC-Team` |
| Scope | All users |
| Reviewer | Members (self review) |
| Duration / recurrence | 3 days, one time |
| Auto apply results | Enabled |
| If reviewers don't respond | No change |

<!-- SCREENSHOT: review settings -->

### Validation

| User | Action | Result |
|---|---|---|
| John SOC | Approved his own access | Kept in the group |
| Sarah SOC | Denied her own access | Removed from the group |
| Omar SOC | No response | Not reviewed, no change |

After verification, Sarah SOC was added back to `SG-SOC-Team` to match the documented lab design.

<!-- SCREENSHOT: John's approval -->
<!-- SCREENSHOT: Sarah's denial -->
<!-- SCREENSHOT: results page showing three outcomes -->

## 5. Audit Evidence

- Reviewed **Entra ID → Monitoring → Audit logs** and confirmed entries for creating the reviews, recording decisions, and removing members from groups.

<!-- SCREENSHOT: audit log entries -->

## Troubleshooting

- Newly created reviews showed **Not started** for a while. A review's start time can lag creation by a few hours, so the reviews were completed once they changed to **In progress**.
- The first attempt at the guest review left External Auditor as **Not reviewed**. <!-- ADD: what caused this and how you fixed it -->
- Role reviews could not be found in the main **Access reviews** page. They are created from **PIM → Microsoft Entra roles → Access reviews**.

## Limitations

- Governance features that are specific to guests (inactive-guest reviews, guest-scoped entitlement policies) require the tenant to be linked to an Azure subscription for guest billing. This lab did not link a subscription, so those features were not used.

## Result

✅ Guest, role, and internal group access reviews configured and completed, with decisions applied and verified.

## Key Takeaways

- **Access reviews** recertify access on a schedule so that stale access gets removed instead of accumulating.
- Reviewers can be **selected users, group owners, managers, or the members themselves (self-review)**.
- **Decisions don't change access until the review completes.** A **Deny** removes access when results are applied, and an **Approve** changes nothing.
- **If reviewers don't respond**, the setting decides the outcome: no change, remove access, approve access, or take recommendations.
- A denied guest loses **membership of the group**, but the **guest account remains** in the directory.
- **Role reviews live in PIM** and are completed under **PIM → Review access**. Group and app reviews are completed at `myaccess.microsoft.com`.
- Access reviews require **Microsoft Entra ID P2** (or Entra ID Governance).
