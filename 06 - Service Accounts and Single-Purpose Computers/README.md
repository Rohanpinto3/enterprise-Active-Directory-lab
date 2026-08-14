# 06 - Service Accounts and Single-Purpose Computers

## Overview

In this lab, I created a dedicated Active Directory service account and configured a Windows 10 client as a single-purpose computer.

The client was configured to automatically log in, launch a specific webpage in fullscreen mode, remain active without sleeping, and restrict local logon using Group Policy.

---

## 1. Create Service Account

I created a new Organizational Unit (OU) named **Service Account**.

Inside the OU, I created a dedicated user account named **Website Login** with the username:

`$website-login`

A dedicated account was used for the single-purpose client instead of using a regular user account.

<p align="center">
  <img width="926" height="465" alt="ss1" src="https://github.com/user-attachments/assets/0dfdcd0a-ecda-4a66-8b25-245c8b2d3610" />
</p>

---

## 2. Configure Automatic Logon

On the Windows 10 client, I downloaded the **Microsoft Sysinternals Suite** and opened **Autologon64**.

I configured Autologon64 to automatically log in using the service account created in Active Directory.

<p align="center">
 <img width="851" height="519" alt="ss2" src="https://github.com/user-attachments/assets/24c4d564-b252-49b7-bd1d-2be01818eec2" />
  <img width="1467" height="731" alt="ss3" src="https://github.com/user-attachments/assets/66a53daf-75fb-4d10-a0b1-061a7947041c" />
</p>

I restarted the Windows 10 client to verify that the service account automatically logged in.

<p align="center">
<img width="1837" height="732" alt="ss4" src="https://github.com/user-attachments/assets/33fcb17f-dae7-46e7-a931-f85f62c62c2a" />
</p>

---

## 3. Configure Browser Startup

I configured the browser to automatically open a webpage after the service account logged in.

For this lab, I used the **Nobara Linux** website as the webpage displayed by the client.

<p align="center">
  <img width="1453" height="558" alt="ss5" src="https://github.com/user-attachments/assets/313ff6fe-7708-4e1f-a1d7-d1a1123b2bbd" />
</p>

---

## 4. Configure Fullscreen Mode

To make the client behave like a basic kiosk-style workstation, I configured the browser to launch in fullscreen mode using:

`--start-fullscreen`

I then added the browser to the Windows Startup folder so that it would launch automatically after login.

The Startup folder was opened using:

`Win + R`

and:

` shell:startup`

<p align="center">
  <img width="489" height="234" alt="ss6" src="https://github.com/user-attachments/assets/95dc4326-f63d-42e0-ae85-afde9a12d89b" />
</p>

---

## 5. Prevent Automatic Sleep

Since the computer is intended to continuously display the webpage, I changed the Windows power settings so that the client does not automatically enter sleep mode.

<p align="center">
  <img width="763" height="604" alt="ss7" src="https://github.com/user-attachments/assets/aa6ffefa-5eca-4322-9740-095d4ebd979f" />
</p>

---

## 6. Test Single-Purpose Computer

After restarting the Windows 10 client, the service account automatically logged in and the browser launched the configured webpage in fullscreen mode.

This demonstrated a basic single-purpose workstation where the system automatically starts and displays the required webpage.

<p align="center">
  <img width="1887" height="816" alt="ss8" src="https://github.com/user-attachments/assets/b874e5b7-f535-40dd-9666-37bf97bdda19" />
</p>

---

## 7. Restrict Local Logon Using Group Policy

I created a new Group Policy Object to restrict local interactive access for the service account.

The policy was configured under:

**Computer Configuration → Windows Settings → Security Settings → Local Policies → User Rights Assignment**

I enabled the **Deny log on locally** policy and configured it for the service account.

<p align="center">
  <img width="992" height="500" alt="ss9" src="https://github.com/user-attachments/assets/bdafd420-25ea-480e-a6d5-c797ad57b13d" />
<img width="893" height="676" alt="ss10" src="https://github.com/user-attachments/assets/0c2829f1-3d54-44f2-bf55-b524c55ecc9e" />
</p>

---

## 8. Test the Security Policy

I switched to another user account and attempted to log in to the Windows 10 client.

The login attempt was denied by the configured Group Policy, confirming that the local logon restriction was successfully applied.

<p align="center">
  <img width="575" height="472" alt="ss11" src="https://github.com/user-attachments/assets/76ed1e7d-c9d8-4207-8964-1d695f825f0a" />
</p>

---




















