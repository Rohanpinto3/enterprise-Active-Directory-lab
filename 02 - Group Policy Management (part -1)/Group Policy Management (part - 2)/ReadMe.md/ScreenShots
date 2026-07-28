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

<p align="center">
  <img src="https://github.com/user-attachments/assets/b032951f-1e47-4f1c-90f1-00f476d3be6f" width="48%">
  <img src="https://github.com/user-attachments/assets/43c63ab8-eab9-47c1-8c33-79440752e330" width="48%">
</p>



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

<img width="562" height="410" alt="gpo ss3" src="https://github.com/user-attachments/assets/c7aab425-28af-4486-b257-a1b4f757f0cf" />
<img width="355" height="375" alt="gpo ss4 p1" src="https://github.com/user-attachments/assets/1326a89d-80d7-4628-8a3c-4b84c8d7b640" />
<img width="405" height="370" alt="gpo ss4 p2" src="https://github.com/user-attachments/assets/cedbfdee-9d29-45e2-875c-a6255bd02713" />
<img width="842" height="612" alt="gpo ss5" src="https://github.com/user-attachments/assets/8b28fe7a-7370-4ce1-b3c0-1f234d56d5f8" />
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

<img width="356" height="377" alt="gpo ss6 p1" src="https://github.com/user-attachments/assets/c0ff56ec-7b0e-401f-a821-ff7fcd9e08b5" />
<img width="392" height="367" alt="gpo ss6 p2" src="https://github.com/user-attachments/assets/4030b979-84df-477d-b3a4-04705f01d3cf" />
<img width="977" height="457" alt="gpo ss6 p3" src="https://github.com/user-attachments/assets/ee3be2e7-1128-4a16-9900-63a461531fa3" />
<img width="962" height="340" alt="gpo ss6 p4" src="https://github.com/user-attachments/assets/6396f2ef-1baf-41cb-a82f-e092398b208e" />

---

## Step 4 – Join the Client to the Active Directory Domain

Renamed the Windows 10 client to **COMP01** and joined it to the **roro.local** Active Directory domain.

Domain administrator credentials were used to authorize the domain join.

After successfully joining the domain, the client computer was restarted and authenticated using a domain user account.

### Evidence

<img width="1670" height="806" alt="gpo ss7 p1" src="https://github.com/user-attachments/assets/6002a257-81a4-4927-8b94-6dcc10995c7d" />
<img width="1897" height="842" alt="gpo ss7 p2" src="https://github.com/user-attachments/assets/c0690c36-bf22-4f03-9e1f-770d87c68815" />
<img width="317" height="315" alt="gpo ss7 p3" src="https://github.com/user-attachments/assets/22ce5c0c-3913-4f5a-bd23-183f22f42346" />
<img width="796" height="492" alt="gpo ss7 p4" src="https://github.com/user-attachments/assets/3d7e4d63-58d7-4239-93d1-0a01c14b0440" />
<img width="382" height="267" alt="gpo ss7 p5" src="https://github.com/user-attachments/assets/6fb09c9d-c4f0-42da-8500-3adc89fed087" />
<img width="1917" height="942" alt="gpo ss7 p6" src="https://github.com/user-attachments/assets/ecfaeadb-ff97-4412-90c3-2520cf2a1ec7" />

---

## Step 5 – Deploy Group Policy Objects

Opened the **Group Policy Management Console (GPMC)** and linked the previously created Group Policy Objects to the **USA Organizational Unit**.

The newly joined client computer (**COMP01**) initially appeared inside the default **Computers** container and was moved into the **USA → Computers** Organizational Unit to receive the appropriate policies.

### Evidence

<img width="1915" height="846" alt="gpo ss8 p1" src="https://github.com/user-attachments/assets/252c91a0-7811-4c49-9c8b-cfd2a1a473c9" />
<img width="268" height="626" alt="gpo ss8 p2" src="https://github.com/user-attachments/assets/9c1f9153-d28e-466b-b645-fbd39efd4414" />
<img width="675" height="337" alt="gpo ss8 p3" src="https://github.com/user-attachments/assets/a6b7a9e1-1f33-4c26-9689-f4f1e066ad9d" />
<img width="492" height="393" alt="gpo ss8 p4" src="https://github.com/user-attachments/assets/cf0bde51-af21-4add-8163-5083b382238c" />
<img width="562" height="367" alt="gpo ss8 p5" src="https://github.com/user-attachments/assets/9b5dd19f-bdd0-4ad6-8f71-aa1fd410c424" />

---

## Step 6 – Verify Group Policy Application

After the client was moved into the correct Organizational Unit, the configured Group Policies were applied.

To validate the deployment, the client attempted to open **Control Panel**, which was successfully blocked by the applied Group Policy.

This confirmed that the client had received the assigned policies from the Domain Controller.

### Evidence

<img width="1917" height="916" alt="gpo ss8 p6" src="https://github.com/user-attachments/assets/be116796-34e3-42c1-977d-46f1a8d11c9e" />

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
