# 02 - MFA Authentication Strength and Conditional Access

## Objective
Configure and enforce Multi-Factor Authentication (MFA) using Microsoft Entra Conditional Access.

## 1. Authentication Strengths

Reviewed the built-in authentication strengths:

- Multifactor authentication
- Passwordless MFA
- Phishing-resistant MFA
- <img width="467" height="911" alt="Screenshot 2026-09-24 233043" src="https://github.com/user-attachments/assets/2d1bd962-9437-4c31-bb17-04889bc4a67e" />


Passwordless and phishing-resistant methods were reviewed but not implemented in this lab.

## 2. Conditional Access MFA Policy

### Policy
`LAB - Require MFA Authentication Strength`

### Configuration
- **Users:** Lab user
- **Target resources:** All cloud apps
- **Grant:** Require multifactor authentication
- **Policy state:** On

### Implementation
1. Created the Conditional Access policy.
2. Initially tested the policy in **Report-only** mode.
<img width="1708" height="923" alt="image" src="https://github.com/user-attachments/assets/79e43837-baa9-43a4-9350-3b196b2b80fe" />

4. Verified the sign-in log showed:
   - `Report-only: User action required`
<img width="822" height="291" alt="Screenshot 2026-09-24 234804" src="https://github.com/user-attachments/assets/79f136bb-67a7-49d2-9077-3da7585e07fe" />

5. Changed the grant control to **Require multifactor authentication**.
<img width="1718" height="931" alt="Screenshot 2026-09-24 235243" src="https://github.com/user-attachments/assets/71283706-5662-4cec-ad5d-b824b2c27860" />
   
7. Enabled the policy.
8. Signed in with the lab user using an InPrivate browser session.
<img width="638" height="605" alt="Screenshot 2026-09-24 235404" src="https://github.com/user-attachments/assets/d7989c9e-a704-4cc7-b74e-fd6cbc5a8df4" />

10. Completed the Microsoft Authenticator MFA prompt.
<img width="537" height="622" alt="Screenshot 2026-09-24 235537" src="https://github.com/user-attachments/assets/b37c752f-c293-4c4a-ace5-43783058a91c" />

12. Verified the sign-in and Conditional Access result in the Entra sign-in logs.
<img width="847" height="407" alt="Screenshot 2026-09-25 165439" src="https://github.com/user-attachments/assets/bc8f34a2-2975-443e-8c82-2c6655644f68" />
<img width="805" height="355" alt="Screenshot 2026-09-25 171051" src="https://github.com/user-attachments/assets/8cb5e2cd-54ce-43ee-86bf-8fc16053a2cc" />


### Result
✅ MFA successfully enforced through Conditional Access.

## Key Takeaways

- Conditional Access can enforce MFA for selected users and cloud applications.
- Report-only mode allows policies to be tested before enforcement.
- Authentication strength can define which authentication methods satisfy an access requirement.
- Microsoft Authenticator was used as the MFA method in this lab.
