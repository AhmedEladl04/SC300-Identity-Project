# 01 - Privileged Identity Management (PIM)

## Objective

Replace a permanent role assignment with just-in-time access using Microsoft Entra Privileged Identity Management: eligible assignment, justification, approval, time-limited activation, and audit.

## 1. Starting State

- **User:** Mohamed Dev
- **Role:** Application Developer (assigned in Phase 3, Lab 3)
- **Assignment type:** Permanent, active

<img width="1816" height="793" alt="Screenshot 2026-10-10 151453" src="https://github.com/user-attachments/assets/7f99d956-bb0f-4179-81e8-14f7b3b67cab" />

## 2. Role Settings

### Configuration

| Setting | Value |
|---|---|
| Maximum activation duration | 2 hours |
| Require justification on activation | Yes |
| Require approval to activate | Yes |
| Approver | Lab Global Administrator |
| Eligible assignment expiry | 6 months |

### Implementation

1. Opened **ID Governance → Privileged Identity Management → Microsoft Entra roles → Settings → Application Developer**.
2. Edited the activation and assignment settings as shown above.

<img width="1392" height="891" alt="Screenshot 2026-10-10 151812" src="https://github.com/user-attachments/assets/ae560f77-d589-48ca-8f3b-3949b8d7a03c" />

## 3. Eligible Assignment

### Implementation

1. Created an **Eligible** assignment for Mohamed Dev on the Application Developer role, valid for 6 months.
2. Removed his permanent active assignment.

<img width="406" height="867" alt="Screenshot 2026-10-10 152114" src="https://github.com/user-attachments/assets/59aa1406-cb1f-411f-9f46-aadbe5e3597c" />
<img width="1341" height="646" alt="Screenshot 2026-10-10 152145" src="https://github.com/user-attachments/assets/16f4d7cb-1108-4e5a-99ac-c00209726753" />


## 4. Validation

### Eligible does not grant access

- Signed in as Mohamed Dev in an InPrivate session and attempted to register an application.
- The attempt was blocked with an insufficient privileges error, confirming the role was not active.

<img width="1857" height="913" alt="Screenshot 2026-10-10 152508" src="https://github.com/user-attachments/assets/d2fb1509-2e37-4366-a5d2-fc6b4ee99645" />

### Activation request

1. As Mohamed Dev, opened **PIM → My roles → Eligible assignments** and activated Application Developer for 1 hour with a justification.
2. The request showed as **pending approval**.

<img width="1622" height="455" alt="Screenshot 2026-10-10 152531" src="https://github.com/user-attachments/assets/c13e6b99-15f3-4d61-8e17-2d068bdff317" />

### Approval

1. As the Global Administrator, opened **PIM → Approve requests**.
2. Approved the request with a justification.

<img width="1611" height="667" alt="Screenshot 2026-10-10 152653" src="https://github.com/user-attachments/assets/efe3206d-a245-43a3-9d8c-5183c1d24be2" />

### Using the activated role

1. Mohamed Dev signed out and back in.
2. Registered `LAB-App-PIMTest` successfully, then deleted it.

<img width="1542" height="902" alt="Screenshot 2026-10-10 152916" src="https://github.com/user-attachments/assets/34e5fad1-6861-4ae0-9418-706ecb09083b" />
<img width="1571" height="630" alt="Screenshot 2026-10-10 152941" src="https://github.com/user-attachments/assets/9c9c48d0-67e3-4913-bde7-f5721a1c3d99" />

### Audit trail

- Reviewed **PIM → Microsoft Entra roles → Audit history** and confirmed entries for the eligible assignment, the activation request, and the approval.
<img width="1560" height="772" alt="Screenshot 2026-10-10 153058" src="https://github.com/user-attachments/assets/a247a64f-c584-448e-8d21-32260e8ec678" />


## Result

✅ Permanent role converted to eligible, with justified, approved, time-limited activation and a full audit trail.

## Key Takeaways

- **Just-in-time access** removes standing privilege: users hold a role only while they need it.
- **Eligible** means a user may activate a role. **Active** means they hold it now. An eligible assignment alone grants no access.
- Activations are **time-bound** and expire automatically. Eligibility itself can also have an end date.
- **Justification and approval** add accountability. **MFA on activation** (recommended in production) prevents a stolen password from being enough to obtain a role.
- PIM keeps an **audit history** of requests, approvals, and activations.
- **Emergency (break-glass) accounts** are the exception and stay permanently active and excluded from policies. Other administrators should be eligible instead.
- PIM requires Microsoft Entra ID P2.
