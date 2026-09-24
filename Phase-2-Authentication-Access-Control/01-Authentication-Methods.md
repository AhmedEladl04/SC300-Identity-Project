# 01 - Authentication Methods
<img width="1530" height="900" alt="image" src="https://github.com/user-attachments/assets/c9c1289f-89e3-4250-bc66-11e1ed454234" />

## Objective

Configure and test authentication methods in Microsoft Entra ID.

## 1. Microsoft Authenticator

### Configuration

- **Registration Campaign:** Enabled
- **Target:** All users
- **Exclusions:** None
- **Method:** Microsoft Authenticator

### Implementation

1. Enabled the Microsoft Authenticator Registration Campaign.
  <img width="1880" height="902" alt="Screenshot 2026-09-24 224826" src="https://github.com/user-attachments/assets/0e7787b0-f710-4507-98ca-ff22ffc88948" />

3. Signed in with a lab user included in the campaign.
   <img width="853" height="616" alt="Screenshot 2026-09-24 230558" src="https://github.com/user-attachments/assets/bd23e0be-9c2c-4955-8c34-385929c48441" />

5. Completed Microsoft Authenticator registration.
   <img width="790" height="693" alt="Screenshot 2026-09-24 230606" src="https://github.com/user-attachments/assets/11614609-6456-4f84-a230-7c3c9aa02e9e" />
   

7. Verified the method under **User → Authentication methods**.
   <img width="508" height="513" alt="Screenshot 2026-09-24 230702" src="https://github.com/user-attachments/assets/015fc5f4-411f-4422-8f85-ab9051b0111c" />


### Result


✅ Successfully registered Microsoft Authenticator.

---

## 2. Temporary Access Pass (TAP)

### Configuration

- **TAP:** Enabled
- **Target:** All users

### Implementation

1. Enabled Temporary Access Pass.
   <img width="1623" height="710" alt="image" src="https://github.com/user-attachments/assets/7b764889-4bc6-453a-b56c-69bc6c3cae5c" />

3. Created a TAP for a lab user.
   <img width="1641" height="808" alt="image" src="https://github.com/user-attachments/assets/12f22231-cffc-49c4-94c0-a2730506d92b" />

5. Used the TAP to sign in as the lab user.
   <img width="531" height="442" alt="image" src="https://github.com/user-attachments/assets/d1f73723-19d8-4056-8323-86eb611936bd" />

7. Verified that authentication was successful.

### Result

✅ Successfully authenticated using TAP.

---

## 3. FIDO2 / Passkeys

FIDO2/passkeys were reviewed as part of the authentication methods study but were **not implemented in this lab**.

### Result

⬜ Not implemented.

---

## Key Takeaways

- Authentication methods are managed through **Microsoft Entra → Authentication methods**.
- Microsoft Authenticator can be deployed using a Registration Campaign.
- TAP provides temporary authentication that can be used to bootstrap authentication-method registration.
- Authentication-method registration is separate from MFA enforcement.
