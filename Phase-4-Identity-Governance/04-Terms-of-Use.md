# 04 - Terms of Use

## Objective

Require users to accept a terms-of-use document before accessing resources, enforced with Microsoft Entra Conditional Access, and verify the acceptance record.

## 1. Terms of Use

### Configuration

| Setting | Value |
|---|---|
| Name | `TOU-Lab-AUP` |
| Display name | Lab Acceptable Use Policy |
| Document | PDF (`Lab-Acceptable-Use-Policy.pdf`), English |
| Require users to expand the terms | On |
| Require consent on every device | Off |
| Expire consents | Off |
| Conditional Access | Custom policy |

### Implementation

1. Prepared a one-page PDF acceptable use policy.
2. Opened **ID Governance → Terms of use → New terms**.
3. Uploaded the PDF and configured the settings above.

<img width="1578" height="412" alt="Screenshot 2026-10-16 191753" src="https://github.com/user-attachments/assets/55f85ef8-4e5f-4a13-831e-0f87316a1a9a" />

## 2. Conditional Access Policy

### Configuration

| Setting | Value |
|---|---|
| Name | `LAB - Require Terms of Use` |
| Users | Lisa HR only |
| Target resources | All cloud apps |
| Grant | Require terms of use: `TOU-Lab-AUP` |
| State | Report-only, then On |

The policy targets a single test user so the administrator account is not affected.

<img width="1558" height="748" alt="Screenshot 2026-10-16 191819" src="https://github.com/user-attachments/assets/9a2701b6-a771-4044-afb4-a706555f1085" />

## 3. Validation

### Report-only

- Signed in as Lisa HR. The terms were not shown, because the policy was not enforced.
- The sign-in log (**Report-only** tab) showed `LAB - Require Terms of Use` being evaluated.

<img width="1596" height="455" alt="Screenshot 2026-10-16 192611" src="https://github.com/user-attachments/assets/7fa5d55f-2e00-44d2-9f05-35b92a2fdf69" />



### Enforced

1. Set the policy to **On**.
2. Signed in as Lisa HR in a new InPrivate session.
3. The terms of use screen appeared before access was granted. Opened the document and selected **Accept**.
4. Lisa HR then reached `myapplications.microsoft.com`.

<img width="1577" height="875" alt="image" src="https://github.com/user-attachments/assets/f7e4d9e6-56c6-4320-b1a7-4c54ad238e60" />
<img width="1805" height="695" alt="Screenshot 2026-10-16 190220" src="https://github.com/user-attachments/assets/a40dcde7-fc12-4040-ad2d-32265bdc202c" />


### Acceptance record

- **ID Governance → Terms of use → TOU-Lab-AUP** showed Lisa HR as accepted, with the date.
- The sign-in log (**Conditional Access** tab) showed the policy applied and satisfied.
- A second sign-in did not ask for the terms again, because the consent is stored.


<img width="1280" height="60" alt="Screenshot 2026-10-16 192523" src="https://github.com/user-attachments/assets/9c66f175-58d2-45d5-b9f9-a0a0109e2505" />




## Result

✅ Terms of use created, enforced through Conditional Access, accepted by a test user, and verified in the acceptance report and sign-in logs.

## Key Takeaways

- **Terms of use** are PDF documents that users must accept before accessing resources. They are often used for guests, contractors, and regulated data.
- They are enforced with the Conditional Access grant control **Require terms of use**. Creating the terms alone enforces nothing.
- Settings include **expanding the terms**, **consent on every device**, and **consent expiry** (re-acceptance on a schedule).
- Acceptances are **recorded and auditable**: who accepted, when, and from which device.
- Report-only mode allows a policy to be tested before enforcement.
- Terms of use require **Microsoft Entra ID P1 or P2**.
- The same policy can target **Guest or external users**. That scenario was not tested in this lab.
