# Phase 2 - Authentication and Access Management

## Objective

Configure and test Microsoft Entra authentication, MFA, password management, Conditional Access, Identity Protection, and risk-based access controls.

## Phase Structure

| # | Topic | Status |
|---|---|---|
| 01 | Authentication Methods | ✅ Completed |
| 02 | MFA, Authentication Strength & Conditional Access | ✅ Completed |
| 03 | SSPR & Password Protection | ✅ Completed |
| 04 | Conditional Access Report-only & What If | ✅ Completed |
| 05 | Identity Protection | ✅ Completed |
| 06 | Risk-Based Access | ✅ Completed |

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

## 05 - Identity Protection

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

### Result
✅ Identity Protection reviewed and integrated with the Conditional Access lab.

## 06 - Risk-Based Access

Created:

`LAB - Require MFA for Sign-in Risk`

Configuration:

- **Users:** Lab user
- **Target resources:** All cloud apps
- **Sign-in risk:** Medium and High
- **Grant:** Require multifactor authentication
- **State:** Report-only

The policy was validated using the **What If** tool with **High sign-in risk** and appeared under **Policies that will apply**.

### Result
✅ Risk-based Conditional Access successfully configured and validated.

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
- Risk-based Conditional Access

## Phase 2 Completion

**Status: ✅ COMPLETE**

This phase provided hands-on experience configuring and validating authentication and access controls in Microsoft Entra ID using a dedicated lab environment.
