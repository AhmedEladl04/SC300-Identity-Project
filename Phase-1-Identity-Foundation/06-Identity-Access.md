# 06 — Identity Access

## Objective

Configure and validate identity access capabilities in Microsoft Entra ID, including:

- License management
- Device identities
- External users
- Cross-tenant access

---

## 1. License Management

Reviewed Microsoft Entra ID P2 licensing through:

**Microsoft Entra admin center → Billing → Licenses → All products**

<img width="1302" height="527" alt="Screenshot 2026-09-17 235019" src="https://github.com/user-attachments/assets/ebef8f86-0db9-44ac-890a-2d0b440056a8" />


### Group-based licensing model

`SG-SOC-Team`

- John SOC
- Sarah SOC
- Omar SOC

The group can be used to automatically assign the required license to its members.

### Key concept

**Direct licensing**
- License assigned individually to a user.
- Requires manual management.

**Group-based licensing**
- License assigned to a group.
- Members receive the license automatically.
- Simplifies administration and onboarding.
  <img width="1490" height="852" alt="image" src="https://github.com/user-attachments/assets/1b5ec43e-c05b-4e1a-af3f-7af09430b4c0" />


---

## 2. Device Identities

Reviewed:

**Identity → Devices → All devices**

and:

**Identity → Devices → Device settings**

### Device identity types

| Type | Description |
|---|---|
| Microsoft Entra registered | Typically personal/BYOD devices |
| Microsoft Entra joined | Organization-owned device joined directly to Entra |
| Hybrid Microsoft Entra joined | Device joined to on-premises AD and registered with Entra |

No unnecessary devices were created for the lab.
<img width="1402" height="837" alt="Screenshot 2026-09-18 011220" src="https://github.com/user-attachments/assets/c4815119-c82c-468c-85d9-9b9b68e4ca51" />


### Key concept

Entra can evaluate both:

**User identity + Device identity**

This becomes important when implementing Conditional Access policies based on device state or compliance.

---

## 3. External Users

Created an external guest identity:

**External Auditor**

The account is configured as:

- User type: `Guest`
- External identity
- Limited directory access
- No privileged Entra role assigned

### Key concept

A **Member** represents an internal workforce identity.

A **Guest** represents an external identity invited to collaborate with the organization.

Guest access should be controlled according to organizational collaboration requirements.
<img width="1530" height="847" alt="Screenshot 2026-09-18 013112" src="https://github.com/user-attachments/assets/ea962ca7-0ccf-4080-be78-317d40dac555" />



## 4. Cross-Tenant Access

Reviewed:

**External Identities → Cross-tenant access settings**

### Default inbound settings

| Access type | Status |
|---|---|
| B2B collaboration — External users/groups | All allowed |
| B2B collaboration — Applications | All allowed |
| B2B direct connect — External users/groups | All blocked |
| B2B direct connect — Applications | All blocked |
| Trust settings | Disabled |

### Default outbound settings

| Access type | Status |
|---|---|
| B2B collaboration — Users/groups | All allowed |
| B2B collaboration — External applications | All allowed |
| B2B direct connect — Users/groups | All blocked |
| B2B direct connect — External applications | All blocked |

### Key concepts

**Inbound access**

Controls what external users can access when coming **into this tenant**.

**Outbound access**

Controls what users from this tenant can access in **other Entra tenants**.

**Organizational settings**

Allow more specific cross-tenant policies for individual partner organizations instead of relying only on the default configuration.
<img width="1502" height="878" alt="Screenshot 2026-09-18 013159" src="https://github.com/user-attachments/assets/94ff547c-7e04-4963-a4b3-13de828444c8" />


---

