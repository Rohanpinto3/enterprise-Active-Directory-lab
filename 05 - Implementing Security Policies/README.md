# 05 - Implementing Security Policies

## Overview

In this lab, I implemented and tested several Active Directory security policies using Group Policy Management. The lab covered password policies, account lockout policies, user rights assignments, and Fine-Grained Password Policies.

---

## 1. Password Policy

I started with the **Default Domain Policy** and configured the password policy under:

**Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Password Policy**

The following settings were configured:

- Remember 4 passwords
- Maximum password age: 60 days
- Minimum password age: 1 day
- Password complexity: Enabled

### Testing

I tested the policy from the Windows client by creating a user that was required to change their password at first login.

A simple password was rejected because it did not meet the configured password requirements. A stronger password satisfying the complexity requirements was then accepted.

<p align="center">
<img width="448" height="413" alt="isp ss1" src="https://github.com/user-attachments/assets/afcbc8b2-c943-4970-9dd0-73381efb2249" />
<img width="1122" height="578" alt="isp ss1 p2" src="https://github.com/user-attachments/assets/20cb875f-2e23-46ca-b173-72095a2f6b68" />
</p>

<p align="center">
<img width="1154" height="646" alt="isp  ss2" src="https://github.com/user-attachments/assets/88e9d3b2-d3ec-4d87-87e9-052d504da1fe" />
<img width="702" height="558" alt="isp ss2-p2" src="https://github.com/user-attachments/assets/b6611eb2-7639-4125-b0c6-3bcc9ce6cf5e" />
</p>

---

## 2. Account Lockout Policy

Next, I configured an account lockout policy through the **Default Domain Policy**.

The policy was configured with:

- Account lockout duration: 30 minutes
- Account lockout threshold: 3 invalid login attempts
- Reset account lockout counter after: 30 minutes

### Testing

From the Windows client, I intentionally entered an incorrect password three times. The account was then locked according to the configured policy.

<p align="center">
  <img width="1141" height="542" alt="isp ss3" src="https://github.com/user-attachments/assets/734243fc-2a0c-4e01-9790-051f029e9ba5" />
  <img width="819" height="586" alt="isp ss4" src="https://github.com/user-attachments/assets/2f3d07e8-040c-4f77-8543-0d8d72216cd5" />

</p>

<p align="center">
<img width="630" height="492" alt="isp ss5" src="https://github.com/user-attachments/assets/9c1b6695-01f6-4c8d-8454-d480d9042b19" />
</p>

---

## 3. User Rights Assignment

I created a separate GPO for **User Rights Assignment**.

The policy was used to control which users or groups could perform specific logon actions.

### Deny Log on Locally

The **IT** group was added to:

**Deny log on locally**

<p align="center">
<img width="1532" height="724" alt="isp ss6" src="https://github.com/user-attachments/assets/7d3173d3-e5f3-4604-b632-353a9728640e" />
</p>

### Allow Log on Through Remote Desktop Services

I also configured:

**Allow log on through Remote Desktop Services**

and assigned the required group.

<p align="center">
 <img width="1485" height="754" alt="isp ss7" src="https://github.com/user-attachments/assets/d5136f9d-b1b4-47ba-b479-aee70ef5236b" />
</p>

### Testing

I tested the local logon restriction using an account that was not included in the permitted group.

<p align="center">
  <img width="863" height="595" alt="isp ss8" src="https://github.com/user-attachments/assets/e0f881ab-7ab7-41a0-b078-c49ab61fea0c" />
  
</p>

I then configured Remote Desktop on the Windows 10 client and attempted to connect using a regular user account. The connection was denied by the configured policy.

<p align="center">
<img width="1442" height="804" alt="isp ss10" src="https://github.com/user-attachments/assets/6c4d92d8-5526-4174-82dc-9a710a31886a" />
</p>

---

## 4. Fine-Grained Password Policy

The final part of the lab introduced **Fine-Grained Password Policies (FGPP)**.

Unlike the Default Domain Policy password settings, Fine-Grained Password Policies allow different password requirements to be applied to specific users or groups within the same Active Directory domain.

For example, an organization could require stronger password requirements for privileged or sensitive accounts while maintaining different requirements for standard users.

I configured and reviewed a Fine-Grained Password Policy in Active Directory.

<p align="center">
  <img width="818" height="418" alt="isp ss9" src="https://github.com/user-attachments/assets/f2322dd7-b36d-452b-afba-6589790130ee" />
<img width="1910" height="748" alt="isp ss11" src="https://github.com/user-attachments/assets/4c687065-ce45-4bf8-a28c-5ffd3e6ac831" />
</p>

---

## Skills Demonstrated

- Active Directory Security
- Group Policy Management
- Password Policies
- Account Lockout Policies
- User Rights Assignment
- Local Logon Restrictions
- Remote Desktop Access Control
- Fine-Grained Password Policies
- Security Policy Testing

---









