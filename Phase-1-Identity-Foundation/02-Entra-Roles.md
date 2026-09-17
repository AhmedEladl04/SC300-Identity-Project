Create users only .
didnt add any roles yet for all just for user administrator to test.


| User | Department | Job title |
| --- | --- | --- |
| **You** | IT / Security | Global Administrator |
| **Alice Admin** | IT | Identity Administrator |
| **John SOC** | Security Operations | SOC Analyst |
| **Sarah SOC** | Security Operations | SOC Analyst |
| **Omar SOC** | Security Operations | Senior SOC Analyst |
| **Mohamed IT** | IT | IT Administrator |
| **David IT** | IT | IT Support Specialist |
| **Mohamed Dev** | Engineering | Application Developer |
| **Lisa HR** | Human Resources | HR Specialist |
| **Mike Manager** | Management | Department Manager |

<img width="1608" height="807" alt="image" src="https://github.com/user-attachments/assets/5abe84c6-4098-488c-b43a-93a9eec2a77d" />
assign alice a role as user administrator
<img width="1618" height="298" alt="image" src="https://github.com/user-attachments/assets/f4300a9a-c3cc-4285-bde3-f8cb1786fd00" />

log in with alice and try to create a user 
Alice SHOULD be able to:

Manage users
Create users
Update user properties
Reset passwords where permitted
Manage some user-related settings

Alice SHOULD NOT be able to:

Assign herself Global Administrator
Manage everything in the tenant
Perform actions requiring higher privileges

A) create a user with alice:
<img width="1651" height="812" alt="image" src="https://github.com/user-attachments/assets/1fa9be22-719e-4c1a-8ca8-50985b734fc2" />
success
B) reset a password with alice
<img width="1628" height="666" alt="image" src="https://github.com/user-attachments/assets/c5a95de5-a8ae-4c1e-99cd-d643a8edabd7" />
c) Can Alice assign herself Global Administrator 
failed

| Test | Expected |
|------|----------|
| View users | Allowed |
| Create user | Allowed |
| Modify user | Allowed |
| Reset normal user's password | Allowed |
| Assign Global Administrator | Denied |
| Modify tenant-wide privileged configuration | Denied/limited |
