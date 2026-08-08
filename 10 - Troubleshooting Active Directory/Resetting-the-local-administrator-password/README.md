<h1>Resetting-the-local-administrator-password</h1>


<h2>Description</h2>
The goal of this task is to reset the local administrator account by running the Hiren’s Boot CD optical drive on the Windows virtual machine.


<h2>Utilities Used</h2>

- <b>Virtualbox</b>
- <b>virtual machines</b>
- <b>Windows ISO</b> 

<h2>Environments Used </h2>

- <b>Windows 10 OS</b>

<h2>Program walk-through:</h2>

The first thing I did was attatch the Hiren's Boot CD optical drive to the storage of the Client 1 VM.

<img src="https://i.imgur.com/4ISL7rP.png" width="80%" alt="Disk Sanitization Steps"/> 

To make sure the Hiren's boot CD booted with no problems I increased the memory usage for the VM to over 4000 mb. This is because Hiren's boot CD needs more memory to start up because of the amount of data it uses. Another thing I did was I enabled EFI. And lastly I put the optical disk to the top in terms of boot order.

<img src="https://i.imgur.com/SYfldIO.png" width="80%" alt="Disk Sanitization Steps"/> 


After I finished booting up the VM with the newly attactehd Hiren’s Boot CD optical drive. I reset the Admin accounts password that was associated with the Client 1 vm.

<img src="https://i.imgur.com/pR490oy.png" width="80%" alt="Disk Sanitization Steps"/> 

After the password for the Admin account had been reset I logged in without having to enter a password.

<img src="https://i.imgur.com/38zoC6a.png" width="80%" alt="Disk Sanitization Steps"/> 

And once I was inside I changed the password by going to system settings.

<img src="https://i.imgur.com/meLFeB9.png" width="80%" alt="Disk Sanitization Steps"/> 
