# 05 - Managed Identity

## Objective

Use a system-assigned managed identity to let an Azure resource call Microsoft Graph without storing any secret, and compare this with the client secret approach used in Lab 1.

## 1. Environment

### Configuration

- **Subscription:** Azure subscription 1
- **Resource group:** `rg-lab-sc300`
- **Resource:** Logic App (Consumption), `LAB-LogicApp-MI`

### Implementation

1. Created the resource group `rg-lab-sc300`.
2. Created the Logic App `LAB-LogicApp-MI` on the Consumption plan.

<img width="1725" height="333" alt="Screenshot 2026-10-10 141637" src="https://github.com/user-attachments/assets/83969ec1-4835-4ff5-8f45-3eb8442ad9a3" />
<img width="1786" height="557" alt="image" src="https://github.com/user-attachments/assets/d925e70f-235d-4e10-b04d-f386dce2a359" />


## 2. System-Assigned Managed Identity

### Implementation

1. Opened **Settings → Identity → System assigned** on the Logic App.
2. Set **Status** to **On** and saved.
3. Recorded the Object (principal) ID.

<img width="1007" height="642" alt="Screenshot 2026-10-10 142151" src="https://github.com/user-attachments/assets/d6c13c1c-9632-434f-9076-6832aab155b0" />

## 3. Workflow

### Configuration

- **Trigger:** When an HTTP request is received
- **Action:** HTTP
  - **Method:** `GET`
  - **URI:** `https://graph.microsoft.com/v1.0/users?$top=3&$select=displayName,userPrincipalName`
  - **Authentication type:** Managed identity (system-assigned)
  - **Audience:** `https://graph.microsoft.com`

The HTTP action contains no client ID, secret, or certificate.

<img width="1882" height="885" alt="Screenshot 2026-10-10 143033" src="https://github.com/user-attachments/assets/fdeb556e-40ae-41fe-969d-fd8172aa061e" />

## 4. Graph Permission Assignment

Managed identities have no permission request list and no portal button for admin consent. The Microsoft Graph application permission `User.Read.All` was assigned to the identity with Microsoft Graph PowerShell:

- Connected with `AppRoleAssignment.ReadWrite.All` and `Application.Read.All` as Global Administrator.
- Looked up the Microsoft Graph service principal and the `User.Read.All` application role.
- Created an app role assignment on the managed identity with `New-MgServicePrincipalAppRoleAssignment`.

The command returned the new assignment for `LAB-LogicApp-MI`.

<img width="1892" height="191" alt="image" src="https://github.com/user-attachments/assets/e681deb1-7788-434d-af32-d9452bb87cd0" />

### Troubleshooting

- The first run of the script failed because PowerShell blocked the Microsoft Graph modules (signing prompt and execution policy). Setting the execution policy to `RemoteSigned` for the current user and importing the modules manually resolved it.

## 5. Validation

- The workflow was run only **after** the permission was assigned, because managed identity tokens are cached and an earlier token would not include the new permission.
- The HTTP action returned **200** with the requested users.

<img width="1582" height="485" alt="Screenshot 2026-10-10 145909" src="https://github.com/user-attachments/assets/75f419e8-810f-449f-8f77-67cbfff70533" />
<img width="1433" height="743" alt="Screenshot 2026-10-10 145942" src="https://github.com/user-attachments/assets/0ee06ba3-b365-43a6-af92-2a3196ed1bf0" />
<img width="1382" height="50" alt="Screenshot 2026-10-10 145951" src="https://github.com/user-attachments/assets/8e1a7aa0-91fc-4f3d-89ad-5881f0e830cc" />


### Verification in Entra

- Opened **Enterprise applications**, filtered by **Managed Identities**, and opened `LAB-LogicApp-MI`.
- The **Permissions** page showed `User.Read.All` granted.

<img width="1597" height="782" alt="Screenshot 2026-10-10 150234" src="https://github.com/user-attachments/assets/b3b4a253-8c5b-4eee-96de-8fb53e3a8eb1" />

## 6. Cleanup

- Deleted the resource group `rg-lab-sc300`, which removed the Logic App and its managed identity.

## Comparison with Lab 1

| | Lab 1: app registration | Managed identity |
|---|---|---|
| Credential | Client secret | None stored anywhere |
| Who manages the credential | You (creation, expiry, rotation) | Azure |
| Risk if leaked | Anyone with the secret can act as the app | Nothing to leak |
| Permission assignment | Request in the portal, then admin consent | Admin assigns the app role directly |
| Where it can be used | Anywhere | Only from the Azure resource it belongs to |

## Result

✅ Logic App called Microsoft Graph using a managed identity with no stored secret.

## Key Takeaways

- A **managed identity** is an identity that Azure creates and manages for a resource, removing the need to store, rotate, or protect a credential.
- **System-assigned** identities belong to one resource and are deleted with it. **User-assigned** identities are separate objects that can be shared across resources.
- A managed identity appears in Entra as a **service principal**, and its permissions are assigned the same way as for any other application.
- Granting an application permission is creating an **app role assignment** on the service principal. The portal button in Lab 1 does the same thing as the script used here.
- Managed identity tokens are **cached**, so permissions should be assigned before the first request.
- Deleting the resource deletes a system-assigned identity, which prevents orphaned identities with leftover permissions.
