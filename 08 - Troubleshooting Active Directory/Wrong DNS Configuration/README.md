# Wrong DNS Configuration – Active Directory Lab Scenario

## Overview
joined client machine.

The goal is to demonstrate the effect of DNS misconfiguration on domain connectivity, authentication, and service discovery, and how to properly diagnose and fix it.

We first tried using `mydomain.com`, but that caused conflicts due to public DNS resolution. The environment was re-built with an isolated internal domain named `igrlab.local`.

---

## Environment
- Domain Controller (DC01): Windows Server with Active Directory Domain Services + DNS
- Client Machine (CLIENT1): Windows 10/11 domain-joined workstation
- Domain: `igrlab.local`
- Internal DNS hosted on Domain Controller
- Isolated virtual lab environment

---

## Initial Working State (Baseline)

Before introducing the issue, full domain functionality was verified.

### Network configuration
<img width="651" height="471" alt="ipconfig working state" src="https://github.com/user-attachments/assets/d5993573-cf29-4315-a49e-4fa073d42f42" />

### DNS resolution
<img width="390" height="130" alt="nslookup working state" src="https://github.com/user-attachments/assets/6ff05fc2-07d1-4a80-b238-fc145531e1fb" />

### Domain controller discovery
<img width="1000" height="196" alt="nltest working state" src="https://github.com/user-attachments/assets/a2956cc5-b0cc-4bcd-bfd2-1a8808112dee" />

---

## Issue Simulation – Wrong DNS Configuration

### Change introduced
The client DNS was changed from the DC IP to non-existing DNS server.

### Impact
- Loss of internet connectivity
- Broken domain name resolution
- AD service discovery issues

### Misconfigured state
<img width="382" height="200" alt="wrong dns configuration" src="https://github.com/user-attachments/assets/63e42354-541e-48fa-b372-4a4e81800b60" />

---

## Troubleshooting Process

### Step 1 – DNS resolution check
`nslookup igrlab.local`

<img width="321" height="279" alt="nslookup investigation" src="https://github.com/user-attachments/assets/447384b5-9e34-4527-a90d-7871a155f9b2" />

Result:
- DNS resolution failed or was inconsistent depending on cache state
- Indicates incorrect DNS server usage

---

### Step 2 – Name resolution test
`ping igrlab.local`

<img width="685" height="104" alt="ping test" src="https://github.com/user-attachments/assets/4d288f5c-eea9-4224-ad2d-2b1e775ab741" />

Result:
- Inconsistent behavior due to cached DNS entries
- Not reliable for AD troubleshooting

---

### Step 3 – Domain controller discovery
`nltest /dsgetdc:igrlab.local`

<img width="516" height="49" alt="image" src="https://github.com/user-attachments/assets/045d24af-f676-483f-8699-c8b9d921a59b" />

Result:
- Domain Controller not discovered when cache was cleared

---

## Critical Observation – Cached Session Behavior

Initial tests showed partial connectivity despite incorrect DNS configuration.

### Cause:
- Cached DNS resolver entries
- Active Kerberos session
- Previously authenticated domain session

### Full failure state
A reboot of the client machine was performed to:
- Clear DNS cache
- Reset Kerberos tickets
- Force fresh domain discovery

After reboot, the issue became fully reproducible.

---

## Root Cause
Incorrect DNS configuration on the client machine:

- External DNS used instead of Domain Controller IP
- Prevented resolution of AD SRV records:
  `_ldap._tcp.dc._msdcs.igrlab.local`

Result:
- Domain Controller discovery failure
- Broken Active Directory communication

---

## Resolution

### Actions taken
- DNS corrected to Domain Controller IP
- DNS cache flushed:
`ipconfig /flushdns`
- Client reboot performed

### Correct configuration
<img width="386" height="177" alt="dns fix" src="https://github.com/user-attachments/assets/f9dda845-2fea-46d6-ba29-7441cadb486d" />

---

## Verification

### Network configuration restored
<img width="706" height="450" alt="image" src="https://github.com/user-attachments/assets/98e3b5c9-dd7f-43ba-bb04-553ecfe277f2" />

### DNS resolution working
<img width="418" height="223" alt="image" src="https://github.com/user-attachments/assets/e8885eee-70ef-49e9-b1d1-dd5fcb5709a3" />

### Domain controller discovery restored
<img width="956" height="212" alt="image" src="https://github.com/user-attachments/assets/1180004a-9850-4966-8eaa-eb046b99b581" />

---
