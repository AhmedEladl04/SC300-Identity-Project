# 02 - Enterprise Application and Assignment

## Objective

Create an enterprise application, restrict access with "Assignment required", assign a security group, configure SAML single sign-on settings, and validate access for an assigned and an unassigned user.

## 1. Enterprise Application

### Configuration

- **Name:** `LAB-App-Internal`
- **Type:** Non-gallery application
- **Assignment required:** Yes
- **Visible to users:** Yes

### Implementation

1. Opened **Entra ID → Enterprise applications → New application → Create your own application**.
2. Created `LAB-App-Internal` as a non-gallery application.
3. Opened **Properties** and set **Assignment required?** to **Yes**.

<img width="1553" height="912" alt="Screenshot 2026-10-03 192324" src="https://github.com/user-attachments/assets/887c72f5-00ad-4dac-98a9-385ad2c403b4" />
<img width="1002" height="830" alt="image" src="https://github.com/user-attachments/assets/e6a87f53-ad50-4c3c-a65b-14d04876ffe4" />


## 2. Group Assignment

### Configuration

- **Assigned group:** `SG-Engineering-Team`
- **Members:** Mohamed Dev

### Implementation

1. Opened **Users and groups → Add user/group**.
2. Selected `SG-Engineering-Team` and assigned it to the application.

<img width="1600" height="628" alt="Screenshot 2026-10-03 192531" src="https://github.com/user-attachments/assets/e5e4c4c8-4f5a-4bb3-b5e8-0beb000a1255" />

## 3. SAML Single Sign-On (Configuration Only)

### Configuration

- **Method:** SAML
- **Identifier (Entity ID):** `https://lab-app.example.com`
- **Reply URL:** `https://lab-app.example.com/saml/acs`

### Implementation

1. Opened **Single sign-on → SAML**.
2. Configured the Basic SAML Configuration with placeholder values.
3. Reviewed **Attributes & Claims**.
4. Noted the signing certificate expiry date.

No service provider exists behind this application, so this section documents the SSO configuration and was not tested with an end-to-end sign-in.

<img width="808" height="368" alt="image" src="https://github.com/user-attachments/assets/8bc85ba4-bae8-4ad5-b119-bfc4b522b0b8" />


## 4. Validation

### Test users

| User | Group membership | Expected result |
|---|---|---|
| Mohamed Dev | `SG-Engineering-Team` (assigned) | Access allowed, app visible in My Apps |
| Lisa HR | Not assigned | Access blocked, app not visible |

### Assigned user (Mohamed Dev)

- Signed in at `myapplications.microsoft.com` using an InPrivate session.
- The `LAB-App-Internal` tile was visible.

<img width="1377" height="551" alt="Screenshot 2026-10-03 194021" src="https://github.com/user-attachments/assets/36719add-ff01-49ea-879e-946b30ccedbd" />

### Unassigned user (Lisa HR)

- Signed in at `myapplications.microsoft.com` using a separate InPrivate session.
- The application tile was not visible.
- Opening the application's User access URL returned error **AADSTS50105** (user is not assigned to a role for the application).

<img width="1653" height="593" alt="Screenshot 2026-10-03 194159" src="https://github.com/user-attachments/assets/1d388c91-7d0e-4046-a716-d0a9381cc061" />
<img width="691" height="383" alt="image" src="https://github.com/user-attachments/assets/b6ff5b53-3453-4dae-9a57-03e3f48bc232" />

### Audit evidence

- The blocked sign-in for Lisa HR with error code `50105` was verified in **Entra ID → Monitoring → Sign-in logs**.

<img width="1548" height="62" alt="image" src="https://github.com/user-attachments/assets/6db4cdb6-d69b-4922-aaa6-3e14e630c7fe" />

## Result

✅ Application access restricted to an assigned group and validated with an allowed and a blocked user.

## Key Takeaways

- **Assignment required** controls who can access an application. When it is off, any user in the tenant can open it. When it is on, only assigned users or groups can.
- Assigning **groups** instead of individuals means access follows group membership and scales better. Group assignment to applications requires Entra ID P1 or P2.
- **Single sign-on** lets users access an application with their Entra identity instead of a separate credential. SAML and OIDC are the common protocols.
- SAML **signing certificates expire**. An expired certificate breaks SSO for all users, so expiry dates should be tracked.
- The sign-in logs provide audit evidence for both allowed and blocked access.
