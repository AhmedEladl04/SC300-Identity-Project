# 04 - App Roles

## Objective

Define custom app roles on an application, assign them to security groups, and validate that Microsoft Entra ID includes the assigned role in the user's sign-in token.

## 1. App Roles

### Configuration

| Display name | Value | Allowed member types |
|---|---|---|
| Report Reader | `Report.Read` | Users/Groups |
| Report Admin | `Report.Admin` | Users/Groups |

### Implementation

1. Opened **Entra ID → App registrations → LAB-App-Reporting → App roles**.
2. Created the `Report Reader` role (`Report.Read`) and enabled it.
3. Created the `Report Admin` role (`Report.Admin`) and enabled it.

<!-- SCREENSHOT: App roles list showing both roles enabled -->

## 2. Role Assignment

### Configuration

| Group | Assigned role |
|---|---|
| `SG-SOC-Team` | Report Reader |
| `SG-IT-Team` | Report Admin |

### Implementation

1. Opened **Entra ID → Enterprise applications → LAB-App-Reporting → Users and groups**.
2. Assigned `SG-SOC-Team` to the `Report Reader` role.
3. Assigned `SG-IT-Team` to the `Report Admin` role.

<!-- SCREENSHOT: Users and groups showing group and role -->

## 3. Test Preparation

The app registration was temporarily configured for token inspection:

- Redirect URI `https://jwt.ms` added under the **Web** platform
- **ID tokens** enabled under implicit grant and hybrid flows

This was for lab testing only and was removed after validation.

<!-- SCREENSHOT: Authentication page showing redirect URI and ID tokens setting -->

## 4. Validation

An authorization request using `response_type=id_token` was opened in separate InPrivate sessions. The resulting ID token was decoded at `jwt.ms`.

| User | Group membership | Expected `roles` claim | Result |
|---|---|---|---|
| John SOC | `SG-SOC-Team` | `Report.Read` | ✅ |
| David IT | `SG-IT-Team` | `Report.Admin` | ✅ |
| Lisa HR | None | No `roles` claim | ✅ |

<!-- SCREENSHOT: decoded token for John SOC (roles claim, identifiers blurred) -->
<!-- SCREENSHOT: decoded token for David IT (roles claim, identifiers blurred) -->
<!-- SCREENSHOT: decoded token for Lisa HR (no roles claim) -->

### Troubleshooting

- The first test attempt did not return a token. The app configuration was re-verified (roles enabled, role assignments present, `https://jwt.ms` redirect URI and **ID tokens** setting saved) and the sign-in URL was regenerated, after which the token was returned.

## 5. Cleanup

- Removed the `https://jwt.ms` redirect URI and disabled the ID tokens setting on the app registration.

## Result

✅ App roles created, assigned to groups, and validated through the `roles` claim in the sign-in token.

## Key Takeaways

- **App roles** define what a user can do inside a specific application. The application defines the roles, and Entra records who holds them.
- Entra includes the assigned role **values** (for example `Report.Admin`) in the token's `roles` claim.
- Entra does **not** enforce roles inside the application. The application must read the claim and apply it.
- Assigning roles to **groups** means access follows group membership. Group assignment to applications requires Entra ID P1 or P2.
- **App roles are not Entra roles.** Entra roles (such as Global Administrator) manage the directory. App roles control access within one application.
- Users with no role assignment receive a token without a `roles` claim.
