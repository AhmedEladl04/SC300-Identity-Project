# 02 - Access Reviews

## Objective

Use Microsoft Entra access reviews to recertify access: a guest user in a group, a privileged role assignment, and an internal group using self-review.

## 1. Preparation

- Created the security group `SG-External-Auditors` and added the guest user **External Auditor** as a member.
- Confirmed `SG-SOC-Team` contains John SOC, Sarah SOC, and Omar SOC.

<img width="1103" height="551" alt="image" src="https://github.com/user-attachments/assets/00beb646-bfd4-455b-a3b7-2286dcbc73db" />

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

<img width="1106" height="426" alt="image" src="https://github.com/user-attachments/assets/e85a4200-6c76-4673-bc8b-3581e3a27f89" />

### Validation

1. Opened the review at `myaccess.microsoft.com → Access reviews`.
2. Selected **Deny** for External Auditor with the reason "Engagement ended".
3. Stopped the review and checked **Results**. The decision was applied.
4. Confirmed that External Auditor was removed from `SG-External-Auditors`, while the guest account still exists under **Users**.

<img width="1517" height="445" alt="Screenshot 2026-10-16 180100" src="https://github.com/user-attachments/assets/40e3d113-3904-47d9-879e-027c3261947e" />
<img width="1097" height="321" alt="image" src="https://github.com/user-attachments/assets/89239aa0-2704-484e-811a-0ef7f0136242" />
<img width="1160" height="331" alt="Screenshot 2026-10-16 180740" src="https://github.com/user-attachments/assets/dbdcd2ad-a480-4fb2-8453-b3ed39633c69" />
<img width="1076" height="457" alt="image" src="https://github.com/user-attachments/assets/895fb9b7-50a1-4b4a-a547-f922ea5b8080" />



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

<img width="1102" height="527" alt="image" src="https://github.com/user-attachments/assets/ff4986cc-4270-4146-a963-0a74a7ef6bf8" />

### Validation

1. Reviewed the assignment under **PIM → Review access**.
2. Approved Mohamed Dev with the reason "Still needed for development work".
3. Stopped the review. With auto apply enabled, the results were applied automatically.
4. Confirmed that Mohamed's eligible assignment was unchanged. Approving a user keeps their access.

<img width="1107" height="442" alt="image" src="https://github.com/user-attachments/assets/94d80191-a893-4ef4-a4fe-5364be416ca2" />
<img width="1122" height="407" alt="image" src="https://github.com/user-attachments/assets/2bdec93c-7a58-4b6d-8822-1590656283ed" />


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

<img width="1013" height="501" alt="image" src="https://github.com/user-attachments/assets/fd048160-1178-4861-b982-8be05e3c5c8a" />


### Validation

| User | Action | Result |
|---|---|---|
| John SOC | Approved his own access | Kept in the group |
| Sarah SOC | Denied her own access | Removed from the group |
| Omar SOC | No response | Not reviewed, no change |

After verification, Sarah SOC was added back to `SG-SOC-Team` to match the documented lab design.

<img width="1615" height="561" alt="Screenshot 2026-10-16 173516" src="https://github.com/user-attachments/assets/91d404b5-5cfd-464f-b9b3-7b2744896e96" />
<img width="1597" height="692" alt="Screenshot 2026-10-16 173652" src="https://github.com/user-attachments/assets/4e5da5ff-9583-474c-a046-dbb2dd6e8f95" />
<img width="901" height="538" alt="Screenshot 2026-10-16 173712" src="https://github.com/user-attachments/assets/d009bde3-0b8c-4de1-861f-f439bf243848" />
<img width="1102" height="467" alt="image" src="https://github.com/user-attachments/assets/17b28863-49e8-4cfe-8753-355a1cfae153" />



## 5. Audit Evidence

- Reviewed **Entra ID → Monitoring → Audit logs** and confirmed entries for creating the reviews, recording decisions, and removing members from groups.

<img width="1617" height="421" alt="Screenshot 2026-10-16 175824" src="https://github.com/user-attachments/assets/e8b5e357-2c27-4251-adc8-04ba15f3629d" />

## Troubleshooting

- Newly created reviews showed **Not started** for a while. A review's start time can lag creation by a few hours, so the reviews were completed once they changed to **In progress**.
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
