# 05 - Identity Protection

## Objective
Review Microsoft Entra Identity Protection and understand user risk, sign-in risk, and risk detections.

## 1. Identity Protection Overview

Reviewed the Identity Protection overview, including:

- Risky users
- Risky sign-ins
- Risk detections

### Lab Status

- **Risky users:** 0
- **Risky sign-ins:** 0
- **Risk detections:** 0

No risky activity was detected in the lab.

## 2. Risk Detections

Reviewed:

**Entra ID → Protection → Identity Protection → Risk detections**

### Result
No risk detection events were present.

## 3. Risk Policies

Reviewed the existing risk remediation policies.

### Sign-in Risk Remediation

- **Users:** All users
- **Sign-in risk:** Low and above
- **Access:** Block access

### User Risk Remediation

- **Users:** All users
- **User risk:** Low and above
- **Access:** Block access

The existing policies were reviewed but not modified.

## 4. Relationship with Conditional Access

Identity Protection risk signals were also used with Conditional Access.

The lab policy:

`LAB - Require MFA for Sign-in Risk`

was configured to respond to **Medium and High sign-in risk** and was validated using the Conditional Access **What If** tool.

## Result

✅ Identity Protection reviewed and its risk signals integrated into the Conditional Access lab.

## Key Takeaways

- **User risk** represents the likelihood that a user's identity has been compromised.
- **Sign-in risk** represents the likelihood that a specific sign-in is risky.
- Identity Protection provides risk signals that can be used by Conditional Access.
- A clean lab may show zero risk detections because no suspicious activity has been detected.
