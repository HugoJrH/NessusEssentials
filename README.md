<h1>Nessus Essentials Vulnerability Management Lab</h1>

<h2>Description</h2>
This is a walkthrough of how I created A Virtual Machine environment using VMWare running Windows 10. I did this project to gain experience with Nessus Essentials and learn how to scan for vulnerabilities and remediate them. This project will showcase two of the main steps in the Vulnerability Management Lifecycle. I will be using Nessus Essentials to scan local VMs hosted on VMWare Workstation in order run credentialed scans to discover vulnerabilities, remediate some of the vulnerabilities, then perform a rescan to verify remediation.
<br />

<h2>Utilities Used</h2>

- <b>Nessus Essentials</b> 
- <b>CMD</b>

<h2>Environments Used </h2>

- <b>VMWare</b>
- <b>Windows 10</b> (21H2)

<h2>Links</h2>

- <b>VMWare Workstation Pro:</b> https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html
- <b>Nessus Essentials:</b> https://www.tenable.com/products/nessus/nessus-essentials
- <b>Windows 10 ISO:</b> https://www.microsoft.com/en-us/software-download/windows10

<h2 align="center">Program walk-through</h2>

<p align="center">
<b>The first thing to do is Download Nessus Essentials, Vulnerability management software. It takes a while to download so, I went ahead and download, Windows 10 .iso on a Virtual Machine and configuring it.</b> <br/>
</p>

![Downloading Nessus](https://github.com/HugoJrH/HugoJrH/assets/126385725/372c1387-cc9a-433d-a0cd-28d9aafa4b43)

<br />
<br />
<p align="center">
<b>For the Virtual Machine that I will be managing vulnerabilities on, I have to configure the network adapter to be bridged so it can be on the same network as my host machine. I do this because Nessus has to Secure Server Login (SSL) into the Virtual Machine and it's just easier if it's using my local network.
  
  Sidenote: Be sure to apply the correct Network Adapter on the VMWARE network settings if not applyed correctly the connection won't be established. </b> <br/>
</p>

![network adapter](https://github.com/HugoJrH/HugoJrH/assets/126385725/62f55ca1-a9bc-4300-ad12-23aa429c3fa3)

<br />
<br />
<p align="center">
<b>While waiting for Nessus to finish, I made sure the VM windows 10 was fully set up and named it 'admin' and made sure it was able to pull an IP; which is needed for the Vulnerable scans. I opened up CMD and typed "ipconfig" which led the IP to be 192.168.0.144 as the screenshot shows.</b> <br/>
</p>

![IP was able to to be pulled](https://github.com/HugoJrH/HugoJrH/assets/126385725/8a01bc47-f227-45d9-b0ea-1fdc6b83d3fe)

<br />
<br />
<p align="center">
<b>If the proper network adapter was selected, the system will be able to ping itself. If a 'Request timed out.' is displayed consider disabling the Windows Firewall on your "VM" shown below and  consider checking the network adapter and make sure it's the correct one.
</b> <br/>
</p>

![connection established](https://github.com/HugoJrH/HugoJrH/assets/126385725/c8228423-7848-40ff-812d-19297dbd2447)

<br />
<br />
<p align="center">
<b>If the Requests Timed Out; Type wf.msc and near the bottom click on 'Windows Defender Firewall Properties' by disabling the windows Firewall circled red, green, and blue, it'll help the VM communicate properly. </b> <br/>
</p>

![Turn off file wall on VM](https://github.com/HugoJrH/HugoJrH/assets/126385725/beb4d3ff-1a7b-4160-a8ee-ad5a40baa20e)
