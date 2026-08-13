# 04 - File Services and Network Sharing

## Overview

In this lab, I configured Windows Server as a basic file server and created a shared network resource for domain users. I also configured network drive mapping through Group Policy and explored storage management using File Server Resource Manager (FSRM).

---

## 1. Create the Shared Folder

I started by creating a folder named `SHARED` on the Windows Server. This folder will be used as the central location for files that need to be accessed over the network.

<p align="center">
 <img width="1130" height="513" alt="fs ss1" src="https://github.com/user-attachments/assets/8ceda729-d77d-4d5e-9a9a-1c284f32e4dd" />
  <img width="647" height="307" alt="fs ss2" src="https://github.com/user-attachments/assets/fc914c70-2ee8-4cc6-9e3f-32fb1ada429a" />
</p>

---

## 2. Configure Network Sharing

I opened the properties of the `SHARED` folder and went to **Sharing → Advanced Sharing**.

I enabled **Share this folder**, which makes the folder accessible over the network using the SMB file-sharing protocol.

I then opened the share permissions and added **Domain Users**, allowing domain users to access the shared resource.

<p align="center">
<img width="360" height="385" alt="fs ss3" src="https://github.com/user-attachments/assets/87f02649-1f27-41a5-8446-4188450e8c7b" />
  <img width="352" height="390" alt="fs ss3 p-2" src="https://github.com/user-attachments/assets/37d37cd7-bb91-479d-9fa4-c1238b7cc4f8" />
</p>

<p align="center">
  <img width="442" height="476" alt="fs ss4" src="https://github.com/user-attachments/assets/2e9fc49d-1862-4709-98ec-3ead40e286e4" />
  <img width="675" height="487" alt="fs ss5" src="https://github.com/user-attachments/assets/50e94412-3df3-4100-8d53-b13a1b9cbb4a" />
  <img width="450" height="472" alt="fs ss 5 p-2" src="https://github.com/user-attachments/assets/ec8c10bd-994a-4adf-8265-35b470d53523" />
</p>

### NTFS Permissions

I also examined the **Security** tab of the shared folder. NTFS permissions provide another layer of access control and work together with share permissions to determine what users can do with files and folders.

---

## 3. Map the Network Drive

I then accessed the shared folder from the Windows 10 client by mapping it as a network drive.

I used the `S:` drive letter and needed the Windows Server hostname to create the network path. I obtained the hostname from the server using:

```cmd
hostname
```

<p align="center">
 <img width="449" height="256" alt="FS SS6" src="https://github.com/user-attachments/assets/7c39d479-77cb-48bf-a352-8332d104a670" />
  <img width="611" height="370" alt="fs ss7" src="https://github.com/user-attachments/assets/987f17e3-2fa1-47db-a215-f16c454eb470" />
</p>



The `SHARED` folder was then available on the Windows 10 client as the `S:` drive.

<p align="center">
<img width="1658" height="396" alt="fs ss8" src="https://github.com/user-attachments/assets/a3df028d-e778-47d7-864e-8bdc2c039c37" />
</p>

This manual mapping method is **non-persistent**, meaning the drive mapping can be lost after the client is restarted.

---

## 4. Create a Persistent Drive Mapping with Group Policy

To automate the drive mapping, I created a **Mapped Drives** Group Policy Object using Group Policy Management.

The drive mapping was configured under:

**User Configuration → Preferences → Windows Settings → Drive Maps**

I configured:

* Drive Letter: `S:`
* Label: `SHARED`
* Location: Windows Server network share

The GPO was then linked to the appropriate Organizational Unit.

<p align="center">
<img width="387" height="147" alt="fs ss9" src="https://github.com/user-attachments/assets/8c813e40-27be-4b1b-ba12-c80608419563" />
 <img width="787" height="462" alt="fs ss9-2" src="https://github.com/user-attachments/assets/de9e9292-0630-4f5c-84a3-a2fcf06e3368" />
</p>

<p align="center">
  <img width="781" height="460" alt="fs ss10" src="https://github.com/user-attachments/assets/ed9cb28a-4c67-4241-845f-fec1fed5e178" />
 <img width="1813" height="543" alt="fs ss11" src="https://github.com/user-attachments/assets/1777d9af-8010-4c39-83bf-53306d942d6d" />
</p>

Unlike the manual mapping method, the Group Policy method allows the network drive to be automatically configured for users in the targeted OU and remain available after a reboot.

---

## 5. File Server Resource Manager (FSRM)

The next part of the lab focused on controlling storage usage and the types of files that can be stored on the server.

FSRM was not installed initially, so I added it through **Server Manager**.

<p align="center">
  <img width="652" height="545" alt="fs ss12" src="https://github.com/user-attachments/assets/84c9abdf-153e-4c9f-a248-4285bf11b5bc" />
</p>

### Quota Management

I used **Quota Management** to create a storage quota for the shared folder.

A custom threshold of **80%** was configured, along with an email notification for the IT administrator when the quota reaches the configured threshold.

This provides a way to monitor and control how much storage users consume on the file server.

<p align="center">
  <img width="402" height="395" alt="fs ss13" src="https://github.com/user-attachments/assets/2be702b6-5886-403d-9b26-118bab06bbcd" />
</p>

### File Screening

I then configured **File Screening Management** to control which types of files can be stored on the server.

The file screening configuration was set to block selected categories:

* Audio files
* Video files
* Image files
* Compressed files

This can help organizations control storage usage and prevent certain types of files from being stored on shared file servers.

<p align="center">
  <img width="495" height="486" alt="fs ss14" src="https://github.com/user-attachments/assets/23eafd7b-990a-48da-b955-067a2f9e9eaa" />
</p>

---

## Skills Demonstrated

* Windows Server File Services
* SMB Network Sharing
* Share Permissions
* NTFS Permissions
* Network Drive Mapping
* Group Policy Drive Mapping
* Active Directory Integration
* File Server Resource Manager (FSRM)
* Storage Quotas
* File Screening
* Windows Client Administration

---
















