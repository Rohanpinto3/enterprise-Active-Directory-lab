# Active Directory Deployment

## Overview

This lab demonstrates the initial deployment of an Active Directory environment using Windows Server 2022. The goal was to create a local Active Directory domain and organize it into a scalable structure using Organizational Units (OUs), Security Groups, and User Accounts.

---

## Lab Objectives

- Create a local Active Directory domain
- Access and manage Active Directory using ADUC
- Design an enterprise-style Organizational Unit (OU) hierarchy
- Create Security Groups
- Create User Accounts
- Prepare the environment for future Group Policy management

---

## Environment

| Component | Technology |
|-----------|------------|
| Hypervisor | VMware Workstation |
| Operating System | Windows Server 2022 Standard Evaluation |
| Directory Service | Active Directory Domain Services (AD DS) |
| Management Tool | Active Directory Users and Computers (ADUC) |

---

# Lab Walkthrough

## Step 1 – Windows Server Dashboard

Opened Windows Server and verified the Active Directory management tools were available.


Windows Server Dashboard <img width="1426" height="747" alt="server manager dashboard" src="https://github.com/user-attachments/assets/8644dae6-4279-44b5-ae85-9959f14e6a12" />


---

## Step 2 – Create a Local Active Directory Domain

Created a local Active Directory domain that will serve as the foundation for managing users, groups, computers, and future Group Policy Objects (GPOs).

### Walkthrough Video

https://github.com/user-attachments/assets/12e97fb0-3489-4ed4-88b5-decc26ea7106

---

## Step 3 – Create Organizational Units (OUs)

Created three regional Organizational Units:

- USA
- EUROPE
- ASIA

Each OU represents a separate geographical location within the organization.


<img width="431" height="305" alt="Screenshot 2026-07-08 162227" src="https://github.com/user-attachments/assets/cfe8c696-d158-46df-9732-8ae32ff0d9dd" />)

---

## Step 4 – Design the OU Structure

Each regional OU contains dedicated containers for:

- Users
- Computers
- Servers

This hierarchy provides a clean structure for managing resources and simplifies future Group Policy deployment.

```
Domain
│
├── USA
│   ├── Users
│   ├── Computers
│   └── Servers
│
├── EUROPE
│   ├── Users
│   ├── Computers
│   └── Servers
│
└── ASIA
    ├── Users
    ├── Computers
    └── Servers
```

### Screenshots

<img width="203" height="330" alt="Screenshot 2026-07-08 162454" src="https://github.com/user-attachments/assets/4ac5afc7-c2bc-43f8-9c95-e591fcfe950c" />
<img width="201" height="423" alt="Screenshot 2026-07-08 162624" src="https://github.com/user-attachments/assets/7bfee1cf-7b06-4d46-96cf-d0422ea12680" />





---

## Step 5 – Create Security Groups and User Accounts

Created Security Groups and User Accounts within the Organizational Units to simulate a basic enterprise Active Directory environment.

This organization improves permission management and prepares the domain for future administration tasks.

https://github.com/user-attachments/assets/6f78ee47-805a-457a-913f-c8b56027a8b8

---

## Skills Demonstrated

- Windows Server Administration
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- Organizational Unit (OU) Management
- Security Group Management
- User Account Administration
- Enterprise Directory Organization

---

## Files Included

```
01-active-directory-deployment/
│
├── README.md
├── screenshots/
│   ├── server-dashboard.png
│   ├── create-ou.png
│   ├── ou-structure-1.png
│   └── ou-structure-2.png
```

---

## Next Lab

➡️ **02 - Group Policy Management**

In the next lab, Group Policy Objects (GPOs) will be configured to centrally manage user and computer settings across the Active Directory environment.




















