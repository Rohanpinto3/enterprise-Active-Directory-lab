# Group Policy Not Applying

## Overview
This scenario demonstrates a common Active Directory issue where a Group Policy Object (GPO) is configured correctly but does not apply because the targeted user is located in the wrong Organizational Unit (OU).

The objective was to troubleshoot why a domain user could still access Control Panel despite an active restrictive policy being configured within the domain environment.

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

## Creating Organizational Units and Group Policies

First, a new Organizational Unit called `_GUESTS` was created in Active Directory Users and Computers (ADUC) for demonstration purposes.

<img width="749" height="412" alt="image" src="https://github.com/user-attachments/assets/029a3128-c0cf-4553-ba25-9bfe5c611d0d" />

A new domain user account named `John Johnson` was then created.  
To simulate an administrative oversight, the user was intentionally placed inside the `_USERS` OU instead of `_GUESTS`.

<img width="424" height="278" alt="image" src="https://github.com/user-attachments/assets/87018c7d-fb7d-4db2-9268-8835cb93bdd1" />


Next, a new Group Policy Object named `Disable Control Panel` was created in Group Policy Management.

<img width="158" height="28" alt="image" src="https://github.com/user-attachments/assets/9f20c169-17d2-4a8e-b904-1f2b0018cd7b" />

The following policy was configured:

```text
User Configuration
→ Policies
→ Administrative Templates
→ Control Panel
→ Prohibit access to Control Panel and PC settings
````

<img width="844" height="580" alt="image" src="https://github.com/user-attachments/assets/e2e44fdb-2009-49e4-8792-41511416c4d3" />

The policy was then set to `Enabled`.

<img width="318" height="132" alt="image" src="https://github.com/user-attachments/assets/a91200be-afdb-48f0-9362-a8bb739f3d01" />

Finally, the GPO was linked to the `_GUESTS` Organizational Unit.

<img width="393" height="74" alt="image" src="https://github.com/user-attachments/assets/4a6cafd5-6618-4b5d-8d25-a4dff7a0abc5" />

---

# Initial Working State (Baseline)

The `John Johnson` account was used to log into `CLIENT2`.

Group Policy updates were forced manually using:

```powershell
gpupdate /force
```

<img width="417" height="80" alt="image" src="https://github.com/user-attachments/assets/ebd7d341-bc8a-4867-ac0c-09f23193a52a" />

Despite the restrictive policy existing in the domain environment, Control Panel remained fully accessible.

<img width="1142" height="694" alt="image" src="https://github.com/user-attachments/assets/e7f728ef-47a3-48a6-a8b7-40c194d4adf2" />

This indicated that the policy was not being applied correctly.

---

# Troubleshooting Process

## Step 1 — Verify Applied Policies

The following command was executed:

```powershell
gpresult /r
```

<img width="447" height="48" alt="image" src="https://github.com/user-attachments/assets/8cdd287f-152f-4a07-b83b-36c86ff9db4e" />

The results showed that no domain GPOs were being applied to the user session.

---

## Step 2 — Inspect GPO Scope and User Placement

The Domain Controller was inspected to verify:

* GPO linkage
* Organizational Unit structure
* user placement

The `Disable Control Panel` GPO was correctly linked to the `_GUESTS` OU.

<img width="241" height="112" alt="image" src="https://github.com/user-attachments/assets/681a6850-f08f-4a35-a8d2-10bc667336e9" />

However, the `John Johnson` user account was not located inside the targeted OU.

<img width="746" height="489" alt="image" src="https://github.com/user-attachments/assets/964f1f07-c74a-4028-9e99-3e3e6c987965" />

This prevented the User Configuration policy from applying to the account.

---

## Step 3 — Correct User Placement

The `John Johnson` user account was moved into the `_GUESTS` Organizational Unit.

<img width="362" height="133" alt="image" src="https://github.com/user-attachments/assets/b7c2eb62-ac74-49b6-bdcd-930a4428c4e4" />

---

## Step 4 — Force Group Policy Update

On `CLIENT2`, the following commands were executed:

```powershell
gpupdate /force
gpresult /r
```

<img width="262" height="68" alt="image" src="https://github.com/user-attachments/assets/0695b859-f5a5-4fcd-abd5-a291bcc65c4f" />

The Group Policy Object now appeared in the applied policies list.

Control Panel access was tested once again.

<img width="554" height="127" alt="image" src="https://github.com/user-attachments/assets/116a2666-e224-478b-842e-38b7c745633b" />

As expected, access to Control Panel was successfully blocked.

---

# Root Cause

The Group Policy Object was linked to the `_GUESTS` Organizational Unit, but the targeted user account was located in a different OU.

Because the configured setting was a **User Configuration policy**, the GPO only applied to user objects located within the linked Organizational Unit.

---

# Verification

After moving the user into the correct Organizational Unit and forcing a Group Policy update:

* the policy applied successfully,
* the GPO appeared in `gpresult`,
* Control Panel access was restricted as intended.

---

