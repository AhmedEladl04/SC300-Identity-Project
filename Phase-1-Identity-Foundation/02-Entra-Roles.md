# 02 - Entra Roles

## Objective

Create the lab users, assign a limited administrative role to one of them, and prove that the role grants only what it should (least privilege).

## 1. Lab Users

Ten internal users were created without any roles. The only privileged account at this point was the lab Global Administrator.

| User | Department | Job title |
|---|---|---|
| **Lab Administrator** | IT / Security | Global Administrator |
| **Alice Admin** | IT | Identity Administrator |
| **John SOC** | Security Operations | SOC Analyst |
| **Sarah SOC** | Security Operations | SOC Analyst |
| **Omar SOC** | Security Operations | Senior SOC Analyst |
| **Mohamed IT** | IT | IT Administrator |
| **David IT** | IT | IT Support Specialist |
| **Mohamed Dev** | Engineering | Application Developer |
| **Lisa HR** | Human Resources | HR Specialist |
| **Mike Manager** | Management | Department Manager |

> A job title is only a label on the user object. It grants no permissions. Alice's title says "Identity Administrator", but the role she is given below is **User Administrator**.

<img width="1608" height="807" alt="User list" src="https://github.com/user-attachments/assets/5abe84c6-4098-488c-b43a-93a9eec2a77d" />

## 2. Role Assignment

### Configuration

| Setting | Value |
|---|---|
| User | Alice Admin |
| Role | User Administrator |
| Scope | Directory-wide at this stage (scoped to administrative units later, in [04 - Users, Groups & AU](04-Users-Groups-AU.md)) |

### Implementation

1. Opened **Entra ID → Roles & admins → User Administrator**.
2. Selected **Add assignments** and chose Alice Admin.

No other user was given a role, so the effect of this single assignment could be tested in isolation.

<img width="1618" height="298" alt="Role assignment" src="https://github.com/user-attachments/assets/f4300a9a-c3cc-4285-bde3-f8cb1786fd00" />

## 3. Validation

I signed in as Alice and tried a set of actions. The role should allow day-to-day user management but not privileged or tenant-wide changes.

| Test | Expected | Result |
|---|---|---|
| View users | Allowed | ✅ Allowed |
| Create a user | Allowed | ✅ Allowed |
| Reset a normal user's password | Allowed | ✅ Allowed |
| Assign herself Global Administrator | Denied | ✅ Denied |

### A) Create a user as Alice

Alice created a new user successfully.

<img width="1651" height="812" alt="Alice creates a user" src="https://github.com/user-attachments/assets/1fa9be22-719e-4c1a-8ca8-50985b734fc2" />

### B) Reset a password as Alice

Alice reset a standard user's password successfully.

<img width="1628" height="666" alt="Alice resets a password" src="https://github.com/user-attachments/assets/c5a95de5-a8ae-4c1e-99cd-d643a8edabd7" />

### C) Assign Global Administrator as Alice

Alice tried to assign herself the Global Administrator role. The attempt failed, because User Administrator cannot grant roles.

## Result

✅ A limited role was assigned and verified: Alice can manage users but cannot escalate her own privileges.

## Key Takeaways

- **Least privilege:** give each administrator the smallest role that does the job, not Global Administrator.
- **User Administrator** can create and manage users and reset passwords for non-administrators. It cannot assign roles or change tenant-wide security settings.
- **A job title is not a permission.** Access comes from role assignments and group membership.
- **Testing a role by signing in as that user** is the way to prove what it can and cannot do.
- **Scope matters as much as role.** Assigning the role to administrative units limits Alice to specific users (see 04).
