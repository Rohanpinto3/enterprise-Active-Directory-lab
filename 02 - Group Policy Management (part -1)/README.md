 # 02 - Group Policy Management

## Overview

This lab demonstrates the configuration and management of Group Policy Objects (GPOs) within an Active Directory environment using Windows Server 2022. The objective was to implement common enterprise policies that improve security, standardize user environments, and centrally manage domain users and computers.

---

## Objectives

- Manage Group Policy Objects (GPOs)
- Apply password security policies
- Configure network drive mapping
- Enforce a corporate desktop wallpaper
- Restrict access to Control Panel
- Disable USB storage devices
- Configure account lockout policies
- Verify policy deployment

---

## Environment

| Component | Technology |
|-----------|------------|
| Hypervisor | VMware Workstation |
| Operating System | Windows Server 2022 Standard Evaluation |
| Directory Service | Active Directory Domain Services (AD DS) |
| Management Tool | Group Policy Management Console (GPMC) |

---

To begin the lab, I opened the **Group Policy Management Console (GPMC)** from the Windows Server Start Menu and accessed my Active Directory domain.

### Screenshot

<img width="1897" height="881" alt="group policy win serach" src="https://github.com/user-attachments/assets/e9dd119a-7ec1-4564-bf42-e9ff9a144c0b" />
<img width="786" height="557" alt="gpo domain expanded" src="https://github.com/user-attachments/assets/a9201930-b4f2-44d1-89da-bb30a67bae72" />




---

# Lab Activities


## 1. Password Policy

Configured a Group Policy Object to define password requirements for domain users.

### Purpose

Enforce stronger password security across the domain.


https://github.com/user-attachments/assets/a8b6576b-a749-4447-8cba-243dc3925b53

---

## 2. Drive Mapping

Configured a Group Policy Object for automatic network drive mapping.

### Purpose

Provide users with centralized access to shared network resources.

🎥 Video Demonstration

https://github.com/user-attachments/assets/a2a5f5a6-8ebe-49bd-9396-c0ae1c6832e5

---

## 3. Desktop Wallpaper Policy

Configured a Group Policy Object to assign a standard desktop wallpaper.

### Purpose

Standardize the desktop environment for domain users.


🎥 Video Demonstration

https://github.com/user-attachments/assets/6910e090-76a8-481b-94fb-4a4a7eb516c2

---

## 4. Restrict Access to Control Panel

Configured a policy to restrict access to the Windows Control Panel.

### Purpose

Prevent unauthorized system configuration changes.


🎥 Video Demonstration

https://github.com/user-attachments/assets/44242ff5-841e-42b6-bc06-6ab1d6d264b5

---

## 5. Disable USB Storage

Configured a policy to disable USB storage devices.

### Purpose

Reduce the risk of unauthorized data transfer through removable storage.


🎥 Video Demonstration

https://github.com/user-attachments/assets/8799f946-090d-43fe-9f72-1eab8fcca980

---

## 6. Account Lockout Policy

Configured an account lockout policy for domain user accounts.

### Purpose

Protect against repeated failed sign-in attempts.


🎥 Video Demonstration

https://github.com/user-attachments/assets/f504571a-84c7-498a-9562-dbda2fc61598

---

# Skills Demonstrated

- Group Policy Management
- Group Policy Object (GPO) Configuration
- Password Policy Configuration
- Drive Mapping
- Desktop Environment Management
- Control Panel Restrictions
- USB Storage Restrictions
- Account Lockout Policy Configuration
- Windows Server Administration
- Active Directory Administration

---

# Learning Outcomes

This lab introduced the fundamentals of Group Policy Management in Active Directory. I gained hands-on experience navigating the Group Policy Management Console and configuring several commonly used enterprise Group Policy Objects that are used to manage security and user environments across a Windows domain.













































