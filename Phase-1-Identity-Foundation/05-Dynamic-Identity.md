# 05 — Dynamic Identity & Custom Security Attributes

## Objective

Implement attribute-based dynamic groups and Custom Security Attributes to extend the tenant's identity model.

---

## 1. Dynamic Security Groups

### SG-DYN-SOC-Team

**Membership:** Dynamic User

**Rule:**
```text
user.department -eq "Security Operations"
```
<img width="1480" height="891" alt="Screenshot 2026-09-17 223706" src="https://github.com/user-attachments/assets/3bab1f1e-25dc-441f-a35d-09199f63897f" />


**Expected members:**
- John SOC
- Sarah SOC
- Omar SOC

<img width="1617" height="683" alt="Screenshot 2026-09-17 223814" src="https://github.com/user-attachments/assets/dda28412-c66c-4c7e-b659-041a1dd7f3df" />


### SG-DYN-IT-Team

**Membership:** Dynamic User

**Rule:**
```text
user.department -eq "IT"
```
<img width="1536" height="732" alt="Screenshot 2026-09-17 224004" src="https://github.com/user-attachments/assets/9112490e-c374-44df-9609-c2160242a881" />

**Expected members:**
- Alice Admin
- Mohamed IT
- David IT

<img width="1632" height="798" alt="Screenshot 2026-09-17 224435" src="https://github.com/user-attachments/assets/c6fef62e-6d78-44b3-b099-675f5003dc5c" />


Dynamic groups automatically update membership based on user attributes instead of requiring manual membership management.

---

## 2. Custom Security Attributes
firs assign the attribute definition admin role and attribute assignment admin role 
<img width="1597" height="366" alt="image" src="https://github.com/user-attachments/assets/ef9533a4-4a8e-4571-9390-ddda2780625c" />


Created an attribute set:

**Attribute Set:** `SecurityClassification`

**Attribute:** `AccessLevel`

Example values:

- `Standard`
- `Sensitive`
- `Privileged`

Example lab assignments:

| User | AccessLevel |
|---|---|
| Lab Administrator | Privileged |
| Alice Admin | Privileged |
| John SOC | Standard |
| Sarah SOC | Standard |
| Omar SOC | Standard |
| Mohamed IT | Standard |
| David IT | Standard |
| Mohamed Dev | Standard |
| Lisa HR | Sensitive |
| Mike Manager | Sensitive |



### Important

`AccessLevel` is **metadata**, not a permission.

For example:

```text
AccessLevel = Privileged
```
<img width="1182" height="672" alt="Screenshot 2026-09-17 230728" src="https://github.com/user-attachments/assets/32f7fdae-4c09-4e01-a47a-377aa69632b2" />
<img width="1605" height="480" alt="Screenshot 2026-09-17 230737" src="https://github.com/user-attachments/assets/7d37c9b8-0cff-4654-91fa-c9cb9aaf343e" />

does **not** grant administrative privileges.

Microsoft Entra roles such as `Global Administrator` or `User Administrator` provide administrative permissions.

---



