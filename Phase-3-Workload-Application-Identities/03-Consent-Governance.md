# 03 - Consent Governance and App Registration Control

## Objective

Reduce application-related risk in the tenant by restricting who can register applications, blocking user consent, and providing a controlled admin consent workflow. This addresses the gaps identified in the Phase 1 tenant baseline, where users could register applications.

## 1. Restrict Application Registration

### Configuration

- **Setting:** Users can register applications
- **Before:** Yes (Phase 1 baseline)
- **After:** No

### Implementation

1. Opened **Entra ID → Users → User settings**.
2. Set **Users can register applications** to **No** and saved the change.

<img width="492" height="288" alt="Screenshot 2026-10-03 195543" src="https://github.com/user-attachments/assets/c8bc5feb-d554-4ad2-a6ab-084cad0afdd2" />

### Validation (standard user)

- Signed in as **Lisa HR** (no administrative roles) using an InPrivate session.
- Attempted to create a new app registration.
- The attempt was blocked with an insufficient privileges error.

<img width="805" height="587" alt="Screenshot 2026-10-03 195854" src="https://github.com/user-attachments/assets/3831de81-7955-4fc4-98c7-34ad44ee7978" />

## 2. Least-Privilege Developer Role

### Configuration

- **User:** Mohamed Dev
- **Role:** Application Developer
- **Assignment type:** Active (to be converted to Eligible with PIM in Phase 4)

### Implementation

1. Opened **Entra ID → Roles & admins → Application Developer**.
2. Assigned the role to Mohamed Dev.
3. Signed in as Mohamed Dev and registered `LAB-App-DevTest`, which succeeded.
4. Deleted the test app registration afterwards.

<img width="1597" height="463" alt="Screenshot 2026-10-03 200014" src="https://github.com/user-attachments/assets/e7c35429-992a-44b5-a247-b0a41286a3f2" />
<img width="1831" height="837" alt="Screenshot 2026-10-03 200158" src="https://github.com/user-attachments/assets/27d6521f-ed3d-4db0-b7ee-ebd149bcdb8c" />

## 3. Block User Consent

### Configuration

- **Setting:** User consent settings
- **Value:** Do not allow user consent

### Implementation

1. Opened **Entra ID → Enterprise applications → Consent and permissions → User consent settings**.
2. Selected **Do not allow user consent** and saved.

<img width="1270" height="547" alt="Screenshot 2026-10-03 200307" src="https://github.com/user-attachments/assets/51344837-c7f7-4dd9-a2bf-d65372141e86" />

## 4. Admin Consent Workflow

### Configuration

- **Users can request admin consent:** Yes
- **Reviewer:** Lab Global Administrator

### Implementation

1. Opened **Enterprise applications → Admin consent settings**.
2. Enabled **Users can request admin consent to apps they are unable to consent to**.
3. Added the lab administrator as a reviewer and saved.

<img width="1507" height="731" alt="Screenshot 2026-10-03 200359" src="https://github.com/user-attachments/assets/91552ed3-0fe5-4280-9207-e69bd2399ce6" />

## 5. Validation

### Test application

- **App:** `LAB-App-Consent-Test` (single tenant)
- **Redirect URI:** `https://jwt.ms` (Web)
- **Delegated permission:** Microsoft Graph `Calendars.Read`
- **Admin consent:** Not granted

### User consent attempt

- Lisa HR opened an authorization request for the test application.
- Instead of a consent prompt, the user received **Need admin approval** and submitted an approval request with a justification.

<img width="1083" height="220" alt="Screenshot 2026-10-03 200636" src="https://github.com/user-attachments/assets/21996c5a-ab17-4af6-a849-d2b07f381969" />
<img width="616" height="712" alt="Screenshot 2026-10-03 201514" src="https://github.com/user-attachments/assets/5e403345-d63b-4ace-9a50-4b5a629d8ba8" />
<img width="1267" height="748" alt="Screenshot 2026-10-03 201615" src="https://github.com/user-attachments/assets/2838d945-8f77-415a-b576-ecf21189f5ea" />


### Admin review

- Reviewed the request in **Enterprise applications → Admin consent requests**.
- Denied the request with a reason.
- Verified the related events in **Audit logs**.
<img width="1645" height="492" alt="image" src="https://github.com/user-attachments/assets/f9e54048-0370-4b5e-bff3-a401c8b78bb0" />
<img width="341" height="91" alt="image" src="https://github.com/user-attachments/assets/526803d6-727b-4e56-8551-28d1351910ef" />


### Troubleshooting

- The first attempt to open the authorization URL returned `AADSTS90013: Invalid input received from the user`. The URL had been entered with a placeholder or formatting error. Rebuilding the URL with the correct tenant ID and client ID resolved it.

## Result

✅ Application registration restricted, user consent blocked, and a controlled admin consent workflow validated end to end.

## Key Takeaways

- Allowing every user to register applications or consent to permissions expands the attack surface of the tenant.
- **Illicit consent grant attacks** trick users into approving a malicious application. No password is stolen, so MFA does not prevent it. Restricting user consent is the main defense.
- User consent can be set to none, limited to verified publishers with selected low-risk permissions (recommended), or open to all apps.
- The **admin consent workflow** gives users a controlled way to request access instead of being blocked with no path forward.
- The **Application Developer** role allows app registration without granting broader administrative rights, which supports least privilege.
