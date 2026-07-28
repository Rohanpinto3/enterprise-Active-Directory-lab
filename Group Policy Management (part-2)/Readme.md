# Group Policy Deployment & Testing

## Overview

This lab demonstrates deploying and validating Group Policy Objects (GPOs) in an Active Directory environment. A Windows 10 Enterprise client was configured, joined to the domain, placed into the appropriate Organizational Unit (OU), and used to verify that previously configured Group Policy Objects were successfully applied.

---

## Objectives

- Configure a Windows 10 Enterprise client
- Configure networking between the client and Domain Controller
- Join the client to an Active Directory domain
- Move the client computer into the correct Organizational Unit
- Deploy Group Policy Objects to the client
- Verify that Group Policies are successfully applied

---

## Environment

| Component | Technology |
|-----------|------------|
| Hypervisor | VMware Workstation |
| Domain Controller | Windows Server 2022 |
| Client | Windows 10 Enterprise |
| Directory Service | Active Directory Domain Services (AD DS) |
| Management Tool | Group Policy Management Console (GPMC) |

---

# Lab Walkthrough

## Step 1 – Configure Windows 10 Client

Created a Windows 10 Enterprise virtual machine and selected **Domain Join Instead** during the initial setup. A local client account named **Client1** was created to complete the installation.

### Evidence

- 📷 GPO SS1 – Windows 10 Setup (Domain Join Option)
- 📷 GPO SS2 – Local User Creation (Client1)

---

## Step 2 – Configure the Domain Controller Network

Configured a static IPv4 address on the Windows Server so it could function as the Domain Controller and DNS server.

### Server Network Configuration

| Setting | Value |
|---------|-------|
| IP Address | 192.168.241.129 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.241.2 |

After configuring the network adapter, the configuration was verified using:

```cmd
ipconfig /all
```

### Evidence

- 📷 GPO SS3 – IP Configuration
- 📷 GPO SS4 – Static IPv4 Configuration
- 📷 GPO SS5 – Network Verification

---

## Step 3 – Configure Windows 10 Networking

Configured the Windows 10 client to use the Domain Controller as its preferred DNS server.

### Configuration

- Preferred DNS → Domain Controller (192.168.241.129)
- Alternate DNS → 8.8.8.8

Connectivity between the client and server was verified using:

```cmd
ping 192.168.241.129
```

DNS resolution was tested using:

```cmd
nslookup roro.local
```

### Evidence

- 📷 GPO SS6 P1 – IPv4 Properties
- 📷 GPO SS6 P2 – DNS Configuration
- 📷 GPO SS6 P3 – Ping Test
- 📷 GPO SS6 P4 – NSLookup Verification

---

## Step 4 – Join the Client to the Active Directory Domain

Renamed the Windows 10 client to **COMP01** and joined it to the **roro.local** Active Directory domain.

Domain administrator credentials were used to authorize the domain join.

After successfully joining the domain, the client computer was restarted and authenticated using a domain user account.

### Evidence

- 📷 GPO SS7 P1 – System Properties
- 📷 GPO SS7 P2 – Computer Name Settings
- 📷 GPO SS7 P3 – Domain Join
- 📷 GPO SS7 P4 – Administrator Credentials
- 📷 GPO SS7 P5 – Domain Join Successful
- 📷 GPO SS7 P6 – Domain User Login

---

## Step 5 – Deploy Group Policy Objects

Opened the **Group Policy Management Console (GPMC)** and linked the previously created Group Policy Objects to the **USA Organizational Unit**.

The newly joined client computer (**COMP01**) initially appeared inside the default **Computers** container and was moved into the **USA → Computers** Organizational Unit to receive the appropriate policies.

### Evidence

- 📷 GPO SS8 P1 – Existing Group Policy Objects
- 📷 GPO SS8 P2 – GPOs Linked to USA OU
- 📷 GPO SS8 P3 – Client Located in Default Computers Container
- 📷 GPO SS8 P4 – Moving Client to USA OU
- 📷 GPO SS8 P5 – COMP01 Inside USA Computers OU

---

## Step 6 – Verify Group Policy Application

After the client was moved into the correct Organizational Unit, the configured Group Policies were applied.

To validate the deployment, the client attempted to open **Control Panel**, which was successfully blocked by the applied Group Policy.

This confirmed that the client had received the assigned policies from the Domain Controller.

### Evidence

- 📷 GPO SS8 P6 – Control Panel Access Restricted

---

# Skills Demonstrated

- Active Directory Administration
- Windows Server Administration
- Windows Client Domain Join
- DNS Configuration
- Static IP Configuration
- Organizational Unit Management
- Group Policy Deployment
- Group Policy Validation
- Enterprise Client Management
- Active Directory Troubleshooting

---

# Learning Outcomes

Through this lab, I learned how to integrate a Windows client into an Active Directory domain, configure client-server communication using DNS, deploy Group Policy Objects through Organizational Units, and validate that policies are correctly applied to domain-joined systems. This exercise demonstrates a typical enterprise workflow for managing Windows clients in an Active Directory environment.
