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
  <img src="ScreenShots/isp%20ss1.png" width="48%">
  <img src="ScreenShots/isp%20ss1-p2.png" width="48%">
</p>

<p align="center">
  <img src="ScreenShots/isp%20ss2.png" width="48%">
  <img src="ScreenShots/isp%20ss2-p2.png" width="48%">
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
  <img src="ScreenShots/isp%20ss3.png" width="48%">
  <img src="ScreenShots/isp%20ss4.png" width="48%">
</p>

<p align="center">
  <img src="ScreenShots/isp%20ss5.png" width="60%">
</p>

---

## 3. User Rights Assignment

I created a separate GPO for **User Rights Assignment**.

The policy was used to control which users or groups could perform specific logon actions.

### Deny Log on Locally

The **IT** group was added to:

**Deny log on locally**

<p align="center">
  <img src="ScreenShots/isp%20ss6.png" width="60%">
</p>

### Allow Log on Through Remote Desktop Services

I also configured:

**Allow log on through Remote Desktop Services**

and assigned the required group.

<p align="center">
  <img src="ScreenShots/isp%20ss7.png" width="60%">
</p>

### Testing

I tested the local logon restriction using an account that was not included in the permitted group.

<p align="center">
  <img src="ScreenShots/isp%20ss8.png" width="60%">
</p>

I then configured Remote Desktop on the Windows 10 client and attempted to connect using a regular user account. The connection was denied by the configured policy.

<p align="center">
  <img src="ScreenShots/isp%20ss9.png" width="60%">
</p>

---

## 4. Fine-Grained Password Policy

The final part of the lab introduced **Fine-Grained Password Policies (FGPP)**.

Unlike the Default Domain Policy password settings, Fine-Grained Password Policies allow different password requirements to be applied to specific users or groups within the same Active Directory domain.

For example, an organization could require stronger password requirements for privileged or sensitive accounts while maintaining different requirements for standard users.

I configured and reviewed a Fine-Grained Password Policy in Active Directory.

<p align="center">
  <img src="ScreenShots/isp%20ss10.png" width="60%">
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

## Navigation

⬅️ [03 - File Services and Network Sharing](../03%20-%20File%20Services%20and%20Network%20Sharing/)

➡️ **Next Lab**
