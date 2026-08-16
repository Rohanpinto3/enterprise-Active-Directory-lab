# Network Share Access Denied

## Overview
This scenario demonstrates how insufficient NTFS permissions can prevent a domain user from accessing a shared network folder.

The objective was to simulate a common helpdesk and system administration issue related to shared folder access, group membership, and NTFS permissions.

The troubleshooting and resolution process is also demonstrated.

---

# Environment

- Domain Controller: Windows Server 2019
- Client Machine: Windows 10
- Active Directory Domain: `igrlab.local`
- DHCP Server hosted on Domain Controller
- DNS hosted on Domain Controller
- Oracle VirtualBox lab environment

---

# Environment Setup

## Step 1 — Create Shared Folder

A shared folder was created on the Domain Controller:

```text
C:\Shares\Finance
````

---

## Step 2 — Configure Share Permissions

The folder was shared using Advanced Sharing.

<img width="1131" height="594" alt="image" src="https://github.com/user-attachments/assets/28b25c5d-02fb-4ca1-81c4-780e7daceb5e" />

For simplicity, the share permissions were configured as:

```text
Everyone → Full Control
```

This allowed the scenario to focus specifically on NTFS permissions rather than share-level permissions.

---

## Step 3 — Create Security Group

A security group called `Finance_Users` was created in Active Directory Users and Computers.

<img width="449" height="111" alt="image" src="https://github.com/user-attachments/assets/02c6fc66-0165-444e-af1a-713c3221f258" />

---

## Step 4 — Configure NTFS Permissions

The `Finance_Users` group was added to the folder Security tab with appropriate permissions.

<img width="457" height="251" alt="image" src="https://github.com/user-attachments/assets/c6acd17c-e69d-49b7-8706-bd9cc5011346" />

Inherited permissions were disabled to restrict access exclusively to authorized groups.

<img width="324" height="133" alt="image" src="https://github.com/user-attachments/assets/9faaf93d-1aac-442e-9100-2e07b7fcec88" />

Only administrators and members of `Finance_Users` were allowed to access the folder contents.

---

# Initial Working State (Baseline)

A domain user account (`John Johnson`) attempted to access the shared folder from `CLIENT2`.

Access to the folder contents was denied.

<img width="522" height="189" alt="image" src="https://github.com/user-attachments/assets/a0256352-1d22-4bbc-9288-79e462e3543e" />

---

# Symptoms Observed

The shared folder was visible on the network, but the user was unable to open it due to insufficient permissions.

---

# Troubleshooting Process

## Step 1 — Verify Network Connectivity

Connectivity with the Domain Controller was verified.

```powershell
ping dc
```

<img width="487" height="248" alt="image" src="https://github.com/user-attachments/assets/e8813b26-438b-4466-b5e2-f04e226da7f9" />

---

## Step 2 — Verify Share Availability

The shared folders hosted on the Domain Controller were listed.

```powershell
net view \\dc
```

The `Finance` share was visible.

<img width="413" height="244" alt="image" src="https://github.com/user-attachments/assets/a7f15783-f2fa-4a55-9e0a-918d950fc235" />

---

## Step 3 — Inspect Group Membership

The user account was reviewed in Active Directory Users and Computers under:

```text
User Properties → Member Of
```

It was confirmed that `John Johnson` was not a member of the `Finance_Users` security group.

<img width="403" height="540" alt="image" src="https://github.com/user-attachments/assets/acc206c3-e6a5-412c-bcb2-0d0987dda407" />

---

## Step 4 — Resolution

The user account was added to the `Finance_Users` security group.

<img width="401" height="539" alt="image" src="https://github.com/user-attachments/assets/fe09e26d-c14a-41d0-a1e2-ec8afdea2744" />

The user session was refreshed by logging out and logging back in.

Additional commands used during testing:

```powershell
gpupdate /force
klist purge
```

---

# Root Cause

The user account did not belong to the security group assigned to the NTFS permissions of the shared folder.

---

# Verification

After updating the group membership and refreshing the user session, the shared folder became accessible from `CLIENT2`.

<img width="790" height="601" alt="image" src="https://github.com/user-attachments/assets/72881067-5dbb-46e0-b96b-4988215c157a" />

---
