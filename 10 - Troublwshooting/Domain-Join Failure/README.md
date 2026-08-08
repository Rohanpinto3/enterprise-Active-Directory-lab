# Domain Join Failure Scenario

## Overview

This scenario demonstrates how incorrect DNS configuration can prevent a client machine from joining an Active Directory domain.

The objective was to simulate a domain join failure, identify the root cause using troubleshooting tools, and restore proper communication with the Domain Controller.

---

# Environment

- Domain Controller: Windows Server 2019
- Client Machine: Windows 10
- Active Directory Domain: `igrlab.local`
- DHCP Server hosted on Domain Controller
- DNS hosted on Domain Controller
- Oracle VirtualBox lab environment

---

# Initial Working State (Baseline)

A fresh Windows client machine (`CLIENT2`) was deployed inside the lab environment.

<img width="1020" height="822" alt="image" src="https://github.com/user-attachments/assets/21d62579-286b-4050-8619-4129dc64dd50" />

---

# Issue Simulation

## Change Introduced

The client machine was configured with an incorrect DNS server address:

```text
192.168.222.222
```

<img width="409" height="466" alt="image" src="https://github.com/user-attachments/assets/fa5330e4-5a03-4c8a-bd58-df376bd61c03" />

---

# Symptoms Observed

The client attempted to join the `igrlab.local` domain using:

```text
System Properties > Change Settings > Domain
```

<img width="221" height="61" alt="image" src="https://github.com/user-attachments/assets/805f7bac-4321-451a-8ee5-bde0ebb93568" />

<img width="823" height="789" alt="image" src="https://github.com/user-attachments/assets/8aa81481-23f0-49d7-9337-39289ab4faab" />

The domain join operation failed.

<img width="460" height="175" alt="image" src="https://github.com/user-attachments/assets/a85e09ea-63ac-47ab-8ecf-38d50f8fcab7" />

Error message:

```text
The following error occurred when DNS was queried for the service location (SRV) resource record used to locate an Active Directory Domain Controller for domain "igrlab.local"
```

---

# Troubleshooting Process

## Step 1 - Verify DNS Configuration

Command used:

```powershell
ipconfig /all
```

Observation:
- Incorrect DNS server detected

<img width="652" height="48" alt="image" src="https://github.com/user-attachments/assets/c921a379-0e59-41f7-9edc-4f61583f45ce" />

---

## Step 2 - Test DNS Resolution

Command used:

```powershell
nslookup igrlab.local
```

Result:
- DNS lookup failed

<img width="319" height="149" alt="image" src="https://github.com/user-attachments/assets/9d98cb0a-bc97-46f0-aaad-3beb04633dbf" />

---

## Step 3 - Test Connectivity to Domain Controller

Command used:

```powershell
ping dc.igrlab.local
```

Result:
- Host could not be resolved

<img width="711" height="84" alt="image" src="https://github.com/user-attachments/assets/96c2acd1-9791-4185-ac1c-2dbca44426c5" />

---

## Step 4 - Correct DNS Configuration

Based on the troubleshooting results, the DNS server configuration was corrected to use the Domain Controller.

The client DNS settings were changed back to automatic configuration.

<img width="352" height="89" alt="image" src="https://github.com/user-attachments/assets/765e663f-6465-444d-9e9d-764c291fda23" />

Commands used:

```powershell
ipconfig /renew
ipconfig /all
```

<img width="401" height="21" alt="image" src="https://github.com/user-attachments/assets/e42cf125-d9ca-45e9-b708-321bd7ab24df" />

---

## Step 5 - Verify DNS Resolution

Command used:

```powershell
nslookup igrlab.local
```

Result:
- Domain successfully resolved

<img width="434" height="155" alt="image" src="https://github.com/user-attachments/assets/c6a6ba4b-c083-4c8e-b877-57101f67ce37" />

---

# Root Cause

Incorrect DNS configuration prevented the client machine from locating the Active Directory Domain Controller.

Since Active Directory heavily depends on DNS for domain services and SRV record discovery, the domain join process could not complete successfully.

---

# Verification

After correcting the DNS configuration, the client machine successfully communicated with the Domain Controller and joined the domain.

Windows prompted for domain administrator credentials and completed the join operation successfully.

<img width="757" height="374" alt="image" src="https://github.com/user-attachments/assets/fc4cc6b0-a2d8-46cf-9348-4dc623a0a9c7" />

<img width="274" height="147" alt="image" src="https://github.com/user-attachments/assets/c64cdb7e-7eb0-4f76-9749-c85c8a5f633e" />

---


- IT support troubleshooting workflow
- Root cause analysis
