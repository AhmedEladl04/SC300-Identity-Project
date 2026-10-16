# 04 - Conditional Access Report-only and What If
## Objective
Test and validate Conditional Access policies using Report-only mode, actual sign-ins, sign-in logs, and What If.

## 1. Report-Only Testing

The MFA Conditional Access policy was initially tested in **Report-only** mode.

During a lab user sign-in, the policy showed:

**Report-only: User action required**

This confirmed that the policy was being evaluated.
<img width="1637" height="848" alt="Screenshot 2026-09-25 170432" src="https://github.com/user-attachments/assets/f3f5319e-5c7f-4057-92e1-dcf3381d9767" />
<img width="1616" height="881" alt="Screenshot 2026-09-25 170528" src="https://github.com/user-attachments/assets/b2147694-7dc0-4cdb-89e3-a56fdd34b53b" />
<img width="867" height="318" alt="Screenshot 2026-09-25 171558" src="https://github.com/user-attachments/assets/041c1836-62a8-40f2-99cc-83695051402d" />




## 2. What If

The Conditional Access **What If** tool was used to simulate access scenarios.

The initial simulation returned no applicable policies because the selected conditions did not match the configured policy.

The tool was later used to simulate **High sign-in risk** for the risk-based Conditional Access policy.

### Result
✅ The risk-based policy appeared under **Policies that will apply**.
<img width="1902" height="951" alt="Screenshot 2026-09-25 172131" src="https://github.com/user-attachments/assets/ff16336a-7f31-476a-a997-e734a143947a" />
<img width="1863" height="316" alt="Screenshot 2026-09-25 172137" src="https://github.com/user-attachments/assets/d311517b-e98d-45d2-b164-80381eb57297" />

## Key Takeaways

- Report-only mode allows policies to be tested before enforcement.
- Sign-in logs provide evidence of actual Conditional Access evaluation.
- What If can simulate Conditional Access scenarios without performing an actual risky sign-in.
