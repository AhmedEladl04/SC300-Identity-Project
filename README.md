# SC-300 Identity Project

A hands-on Microsoft Entra ID lab built while preparing for the **SC-300: Microsoft Identity and Access Administrator** exam. Every topic was configured in a real Entra ID P2 tenant, tested, and documented with screenshots.

## Overview

The lab models a small organization with ten internal users and one external guest across five departments: IT, Security Operations, Human Resources, Engineering, and Management. Users are organized into groups and administrative units, and each phase builds on the one before it.

The project covers the four SC-300 areas: managing identities, authentication and access, workload identities, and identity governance.

> This is a lab, not a production environment. Applications are placeholders with no code behind them, and the tenant has a single Entra ID P2 license, which limits some scenarios (see *Not Covered*).

## Project Phases

| Phase | Focus | What was done |
|---|---|---|
| [1 - Identity Foundation](Phase-1-Identity-Foundation/) | Users, roles, groups, administrative units | Tenant baseline, least-privilege admin role tested with a real user, groups and AUs, dynamic groups, custom security attributes, licensing, devices, guest and cross-tenant settings |
| [2 - Authentication & Access Control](Phase-2-Authentication-Access-Control/) | Authentication, MFA, Conditional Access | Authenticator and Temporary Access Pass, MFA through Conditional Access (report-only first), SSPR and banned passwords, What If, Identity Protection and a risk-based policy |
| [3 - Workload & Application Identities](Phase-3-Workload-Application-Identities/) | App registrations, consent, managed identities | Admin consent tested before and after, assignment-required access, consent controls and admin consent workflow, app roles verified in tokens, a managed identity calling Microsoft Graph with no secret |
| [4 - Identity Governance](Phase-4-Identity-Governance/) | PIM, access reviews, entitlement management, terms of use | Just-in-time roles with approval, guest, role, and group reviews, a time-limited access package, terms of use enforced through Conditional Access |

## Highlights

- **Least privilege proven by testing.** A User Administrator could create users and reset passwords but could not give herself Global Administrator.
- **Safe policy rollout.** Conditional Access policies were tested in report-only mode and checked in the sign-in logs before enforcement.
- **Before and after consent test.** The same Graph call returned `403` before admin consent and returned data after it.
- **No stored secrets.** A managed identity called Microsoft Graph with no client secret or certificate anywhere.
- **Consent hardening.** User consent was blocked, with an admin consent workflow as the approved path.
- **Just-in-time and time-limited access.** PIM activation with approval, and an access package that expired automatically.
- **Evidence from the logs.** Sign-in and audit logs were used to confirm results throughout.

## Skills Demonstrated

| Area | Skills |
|---|---|
| Implement identities | Users, groups, administrative units, Entra roles, dynamic groups, custom security attributes, group-based licensing, guest and cross-tenant settings |
| Authentication and access | Microsoft Authenticator, Temporary Access Pass, MFA, authentication strengths, Conditional Access, report-only and What If, SSPR, password protection, Identity Protection |
| Workload identities | App registrations, enterprise applications, Microsoft Graph permissions, admin consent, app roles, managed identities, Microsoft Graph PowerShell |
| Identity governance | PIM, access reviews, entitlement management, terms of use |

## Not Covered

These SC-300 topics were not implemented, because of licensing, cost, or hardware limits:

| Topic | Reason |
|---|---|
| Hybrid identity (Entra Connect / Cloud Sync) | Needs an on-premises environment |
| Application Proxy | Needs an on-premises connector server |
| Conditional Access for workload identities | Needs Workload Identities Premium |
| Lifecycle Workflows | Needs an Entra ID Governance license |
| Guest governance scenarios | Needs a linked Azure subscription for guest billing |
| FIDO2 / passkeys | Needs a hardware security key |
| Log export, KQL, and workbooks | Needs a Log Analytics workspace (Azure cost) |
| Emergency access (break-glass) accounts | Not built in this lab |

## Lab Environment

- Microsoft Entra ID P2 tenant (25-user limit)
- One P2 license, assigned to the administrator. Test users were unlicensed, so licensed-user behaviour was not fully represented
- Microsoft Graph PowerShell for application and managed-identity work
- Screenshots are redacted, and no secrets, tokens, or tenant identifiers are included

## How the Write-ups Are Organized

Each topic follows the same template:

**Objective → Configuration → Implementation → Validation → Result → Key Takeaways**

Start with a phase README for a summary, then open the numbered files for the steps and evidence.

## Author

**Ahmed Eladl**: preparing for the SC-300 exam with this hands-on lab.
