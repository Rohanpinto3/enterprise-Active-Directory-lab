# DHCP Failure / APIPA Scenario

## Overview
This scenario demonstrates how DHCP service failure affects client network connectivity in an Active Directory environment.

The objective was to simulate a DHCP outage, observe client-side symptoms, perform troubleshooting, identify the root cause, and restore proper network functionality.

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

Before introducing the issue, the environment was fully operational.

Verified functionality:
- Successful DHCP lease assignment
- Internet connectivity
- Proper DNS resolution
- Active Directory communication

Commands used:
```powershell
ipconfig
ping www.google.com
```

<img width="978" height="511" alt="image" src="https://github.com/user-attachments/assets/99496c96-d1c8-4a6d-97fe-3cc66d01996d" />

---

# Issue Simulation

## Change Introduced

The DHCP Server service was manually stopped on the Domain Controller.

<img width="886" height="529" alt="image" src="https://github.com/user-attachments/assets/e555b02f-fc7e-4566-8235-4686057e5449" />

---

# Symptoms Observed

The client machine was unable to renew its IP configuration from the DHCP server.

Command used:
```powershell
ipconfig /renew
```

Result:
- DHCP request failed
- Client could not contact DHCP server
- Network connectivity became unavailable

<img width="919" height="166" alt="image" src="https://github.com/user-attachments/assets/c7737680-513b-4d42-8cee-9df535462efc" />

---

# Troubleshooting Process

## Step 1 - Verify DHCP Service Status

The DHCP service status was checked on the Domain Controller.

Observation:
- DHCP service was stopped

---

## Step 2 - Restart DHCP Service

The DHCP service was restarted.

<img width="884" height="529" alt="image" src="https://github.com/user-attachments/assets/9de60485-bd74-4e72-9f90-5a55680e208c" />

<img width="887" height="526" alt="image" src="https://github.com/user-attachments/assets/77cd5cc1-7c43-457e-8003-b1360c8e24a8" />

---

## Step 3 - Verify DHCP Authorization

The DHCP server authorization status was verified in Active Directory.

<img width="309" height="272" alt="image" src="https://github.com/user-attachments/assets/2362dd48-6af8-40e3-b4aa-e20546c5e29a" />

---

## Step 4 - Renew Client IP Configuration

Commands used:
```powershell
ipconfig /release
ipconfig /renew
```

Explanation:
- `/release` removes the current IP lease
- `/renew` requests a new IP address from the DHCP server

---

# Root Cause

The DHCP Server service was unavailable, preventing the client machine from obtaining a valid IP configuration.

As a result:
- the client could not properly communicate with the network
- internet connectivity became unavailable
- domain resource access was disrupted

---

# Verification

After restarting and authorizing the DHCP service, the client successfully obtained a valid IP configuration from the DHCP server.

Network functionality was restored successfully.

Verified functionality:
- Valid DHCP lease obtained
- Internet connectivity restored
- Successful communication with network resources

<img width="950" height="408" alt="image" src="https://github.com/user-attachments/assets/4fb84f26-fa24-4379-9a2b-2d97ef95287f" />

---


