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

<!-- SCREENSHOT: User settings showing "Users can register applications = No" -->

### Validation (standard user)

- Signed in as **Lisa HR** (no administrative roles) using an InPrivate session.
- Attempted to create a new app registration.
- The attempt was blocked with an insufficient privileges error.

<!-- SCREENSHOT: error shown to Lisa HR -->

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

<!-- SCREENSHOT: Application Developer role assignment -->
<!-- SCREENSHOT: successful registration by Mohamed Dev -->

## 3. Block User Consent

### Configuration

- **Setting:** User consent settings
- **Value:** Do not allow user consent

### Implementation

1. Opened **Entra ID → Enterprise applications → Consent and permissions → User consent settings**.
2. Selected **Do not allow user consent** and saved.

<!-- SCREENSHOT: User consent settings -->

## 4. Admin Consent Workflow

### Configuration

- **Users can request admin consent:** Yes
- **Reviewer:** Lab Global Administrator

### Implementation

1. Opened **Enterprise applications → Admin consent settings**.
2. Enabled **Users can request admin consent to apps they are unable to consent to**.
3. Added the lab administrator as a reviewer and saved.

<!-- SCREENSHOT: Admin consent settings -->

## 5. Validation

### Test application

- **App:** `LAB-App-Consent-Test` (single tenant)
- **Redirect URI:** `https://jwt.ms` (Web)
- **Delegated permission:** Microsoft Graph `Calendars.Read`
- **Admin consent:** Not granted

### User consent attempt

- Lisa HR opened an authorization request for the test application.
- Instead of a consent prompt, the user received **Need admin approval** and submitted an approval request with a justification.

<!-- SCREENSHOT: "Need admin approval" page -->
<!-- SCREENSHOT: submitted request -->

### Admin review

- Reviewed the request in **Enterprise applications → Admin consent requests**.
- Denied the request with a reason.
- Verified the related events in **Audit logs**.

<!-- SCREENSHOT: admin consent request and decision -->
<!-- SCREENSHOT: audit log events -->

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
