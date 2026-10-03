# 01 - App Registration

## Objective

Register an application in Microsoft Entra ID, configure a client secret and a Microsoft Graph application permission, and validate the effect of admin consent.

## 1. App Registration

### Configuration

- **Name:** `LAB-App-Reporting`
- **Supported account types:** Single tenant (this directory only)
- **Redirect URI:** None (daemon-style app, no user sign-in)

### Implementation

1. Opened **Entra ID → App registrations → New registration**.
2. Registered `LAB-App-Reporting` as a single-tenant application.
3. Recorded the Application (client) ID and Directory (tenant) ID from the Overview page.

<!-- SCREENSHOT: new app registration / Overview page (blur IDs) -->

## 2. Client Secret

### Configuration

- **Description:** `lab-secret`
- **Expiry:** 90 days

### Implementation

1. Opened **Certificates & secrets → New client secret**.
2. Created the secret and copied the Value immediately (it is shown only once).
3. Stored the secret outside the repository and supplied it to the test script through an environment variable.

<!-- SCREENSHOT: Certificates & secrets page (Value hidden) -->

## 3. Microsoft Graph Application Permission

### Configuration

- **API:** Microsoft Graph
- **Permission type:** Application
- **Permission:** `User.Read.All`

### Implementation

1. Opened **API permissions → Add a permission → Microsoft Graph → Application permissions**.
2. Added `User.Read.All`.
3. Confirmed the status showed **Not granted for tenant**.

<!-- SCREENSHOT: API permissions page before consent -->

## 4. Validation

A PowerShell script requested a token using the client credentials flow and called `GET /v1.0/users`.

### Before admin consent

- The token request succeeded.
- The Graph call returned **403 Forbidden**.

<!-- SCREENSHOT: 403 error -->

### Granting admin consent

1. Selected **Grant admin consent for <tenant>** on the API permissions page.
2. Confirmed the status changed to **Granted for <tenant>**.

<!-- SCREENSHOT: API permissions page after consent -->

### After admin consent

- A fresh token was requested (the earlier token was issued before consent and did not include the permission).
- The Graph call returned users successfully.

<!-- SCREENSHOT: user list returned -->

### Audit evidence

- The consent action was verified in **Entra ID → Monitoring → Audit logs**.

<!-- SCREENSHOT: audit log consent event -->

## 5. App Registration vs. Enterprise Application

| Object | Role |
|---|---|
| **App registration** | The global definition of the application (identity, secrets, permissions requested) |
| **Enterprise application** | The service principal, the tenant-local instance where consent, assignment, and sign-in behavior are managed |

<!-- SCREENSHOT: app registration and the matching enterprise application -->

## Result

✅ Application registered, Graph application permission configured, and admin consent validated with a before/after test.

## Key Takeaways

- **Delegated permissions** act on behalf of a signed-in user. **Application permissions** act as the app itself with no user, which is why they require admin consent.
- Without consent, an app can authenticate but cannot access the resource.
- Tokens issued before consent do not include the new permission, so a fresh token is required.
- A client secret lets anyone holding it act as the app. Certificates or managed identities are preferred for production, and unused secrets should be deleted.
- The app registration is the blueprint; the enterprise application is the local service principal.
