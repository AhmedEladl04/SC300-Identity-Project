# Phase 3 - Workload and Application Identities

## Objective

Configure and govern application identities in Microsoft Entra ID: register applications, control who can access and consent to them, and assign roles within an application.

> `LAB-App-Reporting` and the other applications in this phase are placeholder apps with no code behind them. They exist to demonstrate identity configuration. The roles and permissions model a reporting tool, but nothing is actually built.

## Phase Structure

| # | Topic | Status |
|---|---|---|
| 01 | [App Registration](01-App-Registration.md) | ✅ Completed |
| 02 | [Enterprise Application and Assignment](02-Enterprise-Application.md) | ✅ Completed |
| 03 | [Consent Governance](03-Consent-Governance.md) | ✅ Completed |
| 04 | [App Roles](04-App-Roles.md) | ✅ Completed |

---

## 01 - App Registration

Implemented:

- Single-tenant app registration (`LAB-App-Reporting`)
- Client secret
- Microsoft Graph **application** permission (`User.Read.All`)
- Admin consent

Validated with a PowerShell client credentials request:

- **Before consent:** token issued, Graph call returned `403 Forbidden`
- **After consent:** Graph call returned users

Also compared the app registration with its enterprise application (service principal).

### Result

✅ Application registered and admin consent validated with a before/after test.

---

## 02 - Enterprise Application and Assignment

Implemented:

- Non-gallery enterprise application (`LAB-App-Internal`)
- **Assignment required** set to Yes
- Group assignment (`SG-Engineering-Team`)
- SAML SSO configuration (placeholder values, configuration only)

Validated with two users:

- **Mohamed Dev** (assigned): app visible in My Apps
- **Lisa HR** (not assigned): app hidden, direct access blocked with `AADSTS50105`

### Result

✅ Application access restricted to an assigned group and validated.

---

## 03 - Consent Governance

Implemented:

- Disabled **Users can register applications** (a Phase 1 baseline gap)
- **Application Developer** role for Mohamed Dev
- **Do not allow user consent**
- **Admin consent workflow** with a designated reviewer

Validated:

- Lisa HR could not register an app
- Mohamed Dev could register an app through the Application Developer role
- Lisa HR received **Need admin approval** and submitted a request, which the admin reviewed

### Result

✅ App registration and consent controlled, with a managed approval path.

---

## 04 - App Roles

Implemented:

- Custom app roles on `LAB-App-Reporting`: **Report Reader** (`Report.Read`) and **Report Admin** (`Report.Admin`)
- Role assignment to `SG-SOC-Team` and `SG-IT-Team`

Validated by decoding sign-in tokens:

| User | Group | `roles` claim |
|---|---|---|
| John SOC | `SG-SOC-Team` | `Report.Read` |
| David IT | `SG-IT-Team` | `Report.Admin` |
| Lisa HR | None | No `roles` claim |

### Result

✅ App roles assigned to groups and confirmed in the token.

---

## Not Implemented in This Lab

These topics belong to the workload identity domain but were not built in this lab:

| Topic | What it is | Why it wasn't implemented |
|---|---|---|
| **Managed identities** | Identities for Azure resources that remove the need to store secrets | Requires an Azure subscription and a resource to attach to |
| **Microsoft Entra Application Proxy** | Publishes on-premises web apps through a connector | Requires an on-premises connector server |
| **Conditional Access for workload identities** | Applies location and risk conditions to service principals | Requires Workload Identities Premium licensing |

---

## Key Concepts Demonstrated

- **Delegated vs. application permissions:** delegated acts for a signed-in user, application acts as the app itself and always needs admin consent
- **App registration vs. enterprise application:** the global definition vs. the tenant-local service principal
- **Assignment required** as an access gate, using group assignment
- **Consent controls:** blocking user consent, the admin consent workflow, and protection against illicit consent grants
- **App roles vs. Entra roles:** app roles control access inside one app, Entra roles control the directory
- **Least privilege:** the Application Developer role instead of a broader administrative role

## Phase 3 Skills Practiced

- Application registration
- Client secrets
- Microsoft Graph permissions
- Admin consent
- Enterprise applications
- Application assignment
- SAML SSO configuration
- User consent settings
- Admin consent workflow
- App roles
- Token inspection
- Sign-in and audit log review

## Phase 3 Completion

Status: ✅ COMPLETE

This phase provided hands-on experience registering, securing, and governing application identities in Microsoft Entra ID using a dedicated lab environment.
