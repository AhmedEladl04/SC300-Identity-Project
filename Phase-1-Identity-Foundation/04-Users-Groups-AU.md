# 04 — Users, Groups & Administrative Units

## Administrative Units vs. Security Groups

Administrative Units (AUs) and Security Groups can both contain users, but they serve different purposes.


### Key Difference

| Feature                           | Administrative Unit                          | Security Group                    |
| --------------------------------- | -------------------------------------------- | --------------------------------- |
| Main purpose                      | Administrative scoping                       | Access and membership management  |
| Primary question                  | "Who can be administered within this scope?" | "Who should receive this access?" |
| Can contain users                 | Yes                                          | Yes                               |
| Used for delegated administration | Yes                                          | No, not their primary purpose     |
| Used for access assignment        | Not its primary purpose                      | Yes                               |
| Membership                        | Defines administrative scope                 | Defines group membership          |

A user can belong to both an Administrative Unit and a Security Group because the two objects solve different problems.

---

# Administrative Unit Structure

The lab contains the following Administrative Units:

### AU-IT

**Purpose:** Administrative scope for IT users.

Members:

* Mohamed IT — IT Administrator
* David IT — IT Support Specialist
  <img width="1541" height="495" alt="image" src="https://github.com/user-attachments/assets/08e20b9a-428b-4501-8e9b-3e4598a83c36" />


### AU-Security-Operations

**Purpose:** Administrative scope for the Security Operations team.

Members:

* John SOC — SOC Analyst
* Sarah SOC — SOC Analyst
* Omar SOC — Senior SOC Analyst
  <img width="1572" height="521" alt="image" src="https://github.com/user-attachments/assets/280e2743-76d2-432c-bf23-9e78bdb34497" />


### AU-HR

**Purpose:** Administrative scope for Human Resources.

Members:

* Lisa HR — HR Specialist
  <img width="1597" height="542" alt="image" src="https://github.com/user-attachments/assets/9a5d13a6-4c3e-4b8e-abae-3d2a19b862d6" />


The lab does not create an Administrative Unit for every department because AUs are being used to demonstrate **administrative delegation**, rather than simply representing organizational departments.

---

# Security Group Structure

The lab contains the following security groups:

### SG-SOC-Team

Members:

* John SOC
* Sarah SOC
* Omar SOC

**Purpose:** Represent the Security Operations team for access and resource assignment.

### SG-IT-Team

Members:

* Mohamed IT
* David IT

**Purpose:** Represent the IT team for access and resource assignment.

### SG-HR-Team

Member:

* Lisa HR

**Purpose:** Represent the HR team for access and resource assignment.

### SG-Engineering-Team

Member:

* Mohamed Dev

**Purpose:** Represent the Engineering team for access and resource assignment.

### SG-Management

Member:

* Mike Manager

**Purpose:** Represent the management group for access and resource assignment.

---
<img width="1427" height="756" alt="image" src="https://github.com/user-attachments/assets/5b37f0ad-eec1-4307-b26d-3e3f53d8e468" />


# Current Identity Structure

```text
Microsoft Entra ID Tenant
│
├── Administrative Units
│   │
│   ├── AU-IT
│   │   ├── Mohamed IT
│   │   └── David IT
│   │
│   ├── AU-Security-Operations
│   │   ├── John SOC
│   │   ├── Sarah SOC
│   │   └── Omar SOC
│   │
│   └── AU-HR
│       └── Lisa HR
│
└── Security Groups
    │
    ├── SG-SOC-Team
    │   ├── John SOC
    │   ├── Sarah SOC
    │   └── Omar SOC
    │
    ├── SG-IT-Team
    │   ├── Mohamed IT
    │   └── David IT
    │
    ├── SG-HR-Team
    │   └── Lisa HR
    │
    ├── SG-Engineering-Team
    │   └── Mohamed Dev
    │
    └── SG-Management
        └── Mike Manager
```


Now for delegation:
Set Alice role to be scoped to AU not whole directory

```
You
Global Administrator
│
└── Entire tenant


Alice Admin
User Administrator
│
├── AU-IT
│   ├── Mohamed IT
│   └── David IT
│
├── AU-Security-Operations
│   ├── John SOC
│   ├── Sarah SOC
│   └── Omar SOC
│
└── AU-HR
    └── Lisa HR
```
<img width="1612" height="691" alt="image" src="https://github.com/user-attachments/assets/fa58bd47-76a8-4d4e-849e-c1ee23a16721" />

