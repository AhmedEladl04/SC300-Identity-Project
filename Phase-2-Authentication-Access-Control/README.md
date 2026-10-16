# Phase 2 - Authentication and Access Management

## Objective

Configure and test Microsoft Entra authentication, MFA, password management, Conditional Access, Identity Protection, and risk-based access controls.

## Phase Structure

| # | Topic | Status |
|---|---|---|
| 01 | [Authentication Methods](01-Authentication-Methods.md) | ✅ Completed |
| 02 | [MFA, Authentication Strength & Conditional Access](02-MFA-Authentication-Strength-and-Conditional-Access.md) | ✅ Completed |
| 03 | [SSPR & Password Protection](03-SSPR-and-Password-Protection.md) | ✅ Completed |
| 04 | [Conditional Access Report-only & What If](04-Conditional-Access-Report-only-and-What-If.md) | ✅ Completed |
| 05 | [Identity Protection and Risk-Based Access](05-Identity-Protection.md) | ✅ Completed |

---

## 01 - Authentication Methods

Implemented and reviewed:

- Microsoft Authenticator
- Authenticator Registration Campaign
- Temporary Access Pass (TAP)
- FIDO2/passkeys reviewed but not implemented

### Result
✅ Authentication methods configured and tested.

## 02 - MFA, Authentication Strength & Conditional Access

Reviewed:

- Multifactor authentication
- Passwordless MFA
- Phishing-resistant MFA
- Authentication strengths

Implemented:

- Conditional Access MFA policy
- Lab user targeting
- All cloud apps
- Require multifactor authentication
- Microsoft Authenticator

The policy was initially tested in Report-only mode and was later enabled.

### Result
✅ MFA successfully enforced through Conditional Access.

## 03 - SSPR & Password Protection

Implemented:

- Self-Service Password Reset
- Lab user SSPR testing
- Microsoft Authenticator verification
- Custom banned password list

### Result
✅ SSPR successfully tested and password protection configured.

## 04 - Conditional Access Report-only & What If

Practiced:

- Report-only policies
- Actual CA sign-in validation
- Sign-in logs
- Conditional Access evaluation
- What If simulations

A What If simulation using **High sign-in risk** was used to validate the risk-based Conditional Access policy.

### Result
✅ Conditional Access testing completed.

## 05 - Identity Protection and Risk-Based Access

Reviewed:

- Identity Protection overview
- Risky users
- Risky sign-ins
- Risk detections
- User risk
- Sign-in risk
- Built-in risk remediation policies

### Lab Status

- Risky users: `0`
- Risky sign-ins: `0`
- Risk detections: `0`

No actual risky activity was detected during the lab.

Created a risk-based Conditional Access policy, `LAB - Require MFA for Sign-in Risk`:

- **Users:** Lab user
- **Target resources:** All cloud apps
- **Sign-in risk:** Medium and High
- **Grant:** Require multifactor authentication
- **State:** Report-only

The policy was validated with the **What If** tool using **High sign-in risk** (see 04) and appeared under **Policies that will apply**. It was not triggered by a real risky sign-in.

### Result
✅ Identity Protection reviewed, and a risk-based Conditional Access policy configured and validated with What If.

## Phase 2 Skills Practiced

- Authentication method configuration
- Microsoft Authenticator
- Temporary Access Pass
- MFA
- Authentication strengths
- Self-Service Password Reset
- Password Protection
- Conditional Access
- Report-only policies
- Conditional Access What If
- Sign-in log analysis
- Identity Protection
- User risk
- Sign-in risk
- Risk-based Conditional Access (validated with What If)

## Phase 2 Completion

**Status: ✅ COMPLETE**

This phase provided hands-on experience configuring and validating authentication and access controls in Microsoft Entra ID using a dedicated lab environment.
