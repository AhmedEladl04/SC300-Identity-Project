# 03 — Identity Model

## Objective

Document the identity structure used in the Microsoft Entra ID lab.

## Tenant Identity Model

The lab uses Microsoft Entra ID as the centralized identity
and access management platform.

## Identity Categories

### Privileged Administrative Identities

| User | Role | Purpose |
|---|---|---|
| Lab Administrator | Global Administrator | Tenant administration |
| Alice Admin | User Administrator | User administration |

### Security Operations Identities

| User | Department | Job Title |
|---|---|---|
| John SOC | Security Operations | SOC Analyst |
| Sarah SOC | Security Operations | SOC Analyst |
| Omar SOC | Security Operations | Senior SOC Analyst |

### IT Identities

| User | Department | Job Title |
|---|---|---|
| Mohamed IT | IT | IT Administrator |
| David IT | IT | IT Support Specialist |

### Engineering

| User | Department | Job Title |
|---|---|---|
| Mohamed Dev | Engineering | Application Developer |

### Human Resources

| User | Department | Job Title |
|---|---|---|
| Lisa HR | Human Resources | HR Specialist |

### Management

| User | Department | Job Title |
|---|---|---|
| Mike Manager | Management | Department Manager |

## Identity Principles

- Administrative privileges are assigned through Microsoft Entra roles.
- Users have attributes such as department and job title.
- Groups will later be used to organize users and manage access.
- Dynamic groups will use user attributes for automatic membership.
- Licenses will later be assigned according to organizational requirements.
- External identities will be introduced in a later phase.
