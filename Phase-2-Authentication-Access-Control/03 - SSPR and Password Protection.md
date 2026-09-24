# 03 - SSPR and Password Protection

## Objective
Configure and test Self-Service Password Reset (SSPR) and password protection in Microsoft Entra ID.

## 1. Self-Service Password Reset

### Configuration
- **SSPR:** Enabled
- **Scope:** Lab user
- **Authentication:** Microsoft Authenticator

### Implementation
1. Enabled SSPR for the lab user.
2. Configured the available authentication method.
3. Opened the Microsoft password reset portal using an InPrivate browser.
4. Verified the lab user's identity using Microsoft Authenticator.
5. Successfully reset the user's password.
6. Tested sign-in using the new password.
<img width="1197" height="628" alt="Screenshot 2026-09-05 232136" src="https://github.com/user-attachments/assets/305cd415-b112-4a0e-b405-72973d84c5ed" />
<img width="1612" height="848" alt="Screenshot 2026-09-05 232356" src="https://github.com/user-attachments/assets/fc750162-a42b-4b41-bb08-0d1bca82d4cb" />
<img width="941" height="702" alt="Screenshot 2026-09-05 233246" src="https://github.com/user-attachments/assets/b69c501e-8145-4342-8653-96ac83964500" />
<img width="582" height="361" alt="Screenshot 2026-09-05 233433" src="https://github.com/user-attachments/assets/01731c3e-662d-410b-bbf9-24e8d3545cc6" />


### Result
✅ SSPR successfully configured and tested.

## 2. Password Protection

### Configuration
- **Custom banned password list:** Enabled
- Added custom lab-related passwords to the banned list.

### Implementation
1. Opened **Entra ID → Authentication methods → Password protection**.
2. Enabled the custom banned password list.
3. Added custom passwords to the banned list.
4. Saved the configuration.

### Result
✅ Custom password protection configured.
<img width="872" height="748" alt="image" src="https://github.com/user-attachments/assets/d1f9cf02-53fb-4051-98cf-364a03f75c80" />

## Key Takeaways

- SSPR allows users to reset their own passwords after verifying their identity.
- Conditional Access MFA and SSPR serve different purposes.
- Microsoft Entra Password Protection helps prevent users from choosing weak or organization-specific passwords.
- Custom banned passwords can be added to strengthen password protection.
