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

<br />
<br />
<p align="center">
<b>After Nessus has downloaded, you want to create a new scan, then select 'Basic Network Scan'. </b> <br/>
</p>

![new scan](https://github.com/HugoJrH/HugoJrH/assets/126385725/f8e3c361-f3a0-4598-9f02-e64b8c15cf53)

![basic network scan](https://github.com/HugoJrH/HugoJrH/assets/126385725/c0127118-38fc-4730-8ea8-69ce659ee31c)


<br />
<br />
<p align="center">
<b>After naming the scan, I also put the targeted VM's IP: 192.168.0.144 to be the target for this scan.</b> <br/>
</p>

![Name the scan and set the target ips](https://github.com/HugoJrH/HugoJrH/assets/126385725/f830e35d-c4e7-483f-86f5-e95908532821)

<br />
<br />
<p align="center">
<b>I then lauch the scan by clicking the grey check mark and it's mow scanning for vulnerabilities. When the grey check mark appears the scan has now been completed.</b> <br/>
</p>

https://github.com/HugoJrH/HugoJrH/assets/126385725/a6a1f47f-6e13-4df2-96e7-ddda320b534b

![completed scan](https://github.com/HugoJrH/HugoJrH/assets/126385725/9f20bc93-e8b2-4936-9de2-ccb7ad7b1213)

After the scan completed, it showed 32 results, 31 of which are INFO and 1 LOW. If this was an actual production environment these most likely would be left alone. The Info results are probably because some things don't have proper credentials and are not essentially vulnerabilities.

![HOW MANY RESULTS](https://github.com/HugoJrH/HugoJrH/assets/126385725/69967ad3-8339-41ce-be1e-fbdf8e7407b2)

Looking at one of the INFO results you can see that the Target Credential Status By Authentication Procotol was triggered because we did not actually provide any credentials for this scan.

![image](https://github.com/HugoJrH/VulnerabilityManagement/assets/126385725/b1865c59-4bc7-4bf3-a536-7396dbe02ce0)

Now I'll configure the VM having it able to accept Authenticated Scans and provide credentials to Nessus. 
 I will then rescan the VM and compare the results. I go to services.MSC to start this process and enable Remote Registry. This will allow Nessus to connect to the VM's registry and properly scan for vulnerabilities such as insecure connections or deprecated cipher suites. I'm following these steps from Nessus and what they recommend to actually do credentialed scans. There might be a better way to do this.
![services](https://github.com/HugoJrH/HugoJrH/assets/126385725/92557d3e-2b3d-4fab-932e-6053294876f4)
![remote services](https://github.com/HugoJrH/HugoJrH/assets/126385725/2685fc85-bc70-4c3f-838a-9fca22a30f59)


From there I go to User Account Controls and disable it. I have to do this because this VM is not on a domain so I kind of have to do hacker stuff to get it to work properly. I would never do this in an actual organization or production environment.

![USER ACCOUNT](https://github.com/HugoJrH/HugoJrH/assets/126385725/a0653243-80b1-4400-bd69-fc4a015f8936)
![TURN OFF NOTIFY](https://github.com/HugoJrH/HugoJrH/assets/126385725/0246406c-796f-4e8d-996d-93ba58b42cac)

Next open the registry and add a key that is suppose to allow Nessus to connect in by further disabling user account controls.

![registry](https://github.com/HugoJrH/HugoJrH/assets/126385725/f52288a7-3619-4e04-9590-8321895622d5)
![registry location](https://github.com/HugoJrH/HugoJrH/assets/126385725/69b07259-8f99-4fb2-a5c7-164fda4e2ed9)


Now I navigate the Registry to the file that Nessus instructs us to (highlighted Yellow in the search bar) and I have to add a DWORD value and name it LocalAccountTokenFilterPolicy and give it a value of 1.

![VALUE NAME](https://github.com/HugoJrH/HugoJrH/assets/126385725/f3fca895-8466-450a-8fe2-652ecd36806d)

After the VALUE is set to "1" restart the "VM"
With the registry configured, it is now time to go back into Nessus and configure the scan I created. I have to add the Credentials to the scan so it can work properly. The credentials I'm talking about is the username and password of the VM. This will allow Nessus to use those credentials in places where it is required in the VM registry.

![NEW SCAN NESSUS](https://github.com/HugoJrH/HugoJrH/assets/126385725/e551eca7-2453-40fa-8ca0-fde788d7d7af)
![CONFIGURE](https://github.com/HugoJrH/HugoJrH/assets/126385725/cbdd250c-801e-4cc2-8dac-86d59166a523)

After the scan is properly configured with the right credentials, I run it again.

![Scanning with credentials](https://github.com/HugoJrH/HugoJrH/assets/126385725/d72fc4d7-5031-442a-81c7-1874c82988e3)

This new scan has given us a lot more vulnerabilities than the first one because it is able to scan deeper into the VM due to having credentials. The top picture is the new credentialed scan and the bottom picture is from the first non-credentialed scan. Most of the vulnerabilities found is probably because the version of Windows 10 this VM is running is not up to date.
![CRED SCAN](https://github.com/HugoJrH/HugoJrH/assets/126385725/e9fe253d-32c3-4520-b465-9cc621f33f14)
![HOW MANY RESULTS](https://github.com/HugoJrH/HugoJrH/assets/126385725/697b7fc0-d023-407e-8814-02255dd54c07)

To check the capability of the Nessus scanner, I'm going to download a very old version of Firefox which probably has many vulnerabilities and see if Nessus can discover them (No doubt it will.)


After a deprecated version of Firefox is downloaded, I run another scan. We can see many new alerts and vulnerabilities just from Firefox! 80 Critical!
![FIREFOX](https://github.com/HugoJrH/HugoJrH/assets/126385725/103715cb-b9e0-49f8-983f-e248e20d8794)

A comparison between scans to show the progression of alerts and vulnerabilities.

![ALLLLL](https://github.com/HugoJrH/HugoJrH/assets/126385725/f59ad08c-4344-4db6-9a9d-658c3841bd70)



Showing what some of the alerts and vulnerabilites look like. We can see most of the Critical alerts are just from Firefox. A few ways we can remediate some of the vulnerabilities is by either Updated Firefox, which will probably remediate a lot of them, or we can simply delete Firefox.
![ERRRROORR](https://github.com/HugoJrH/HugoJrH/assets/126385725/58627e88-2234-49d3-8851-13c5788421c1)



To start the process of remediating vulnerabilities, I elect to just delete Firefox. That will instantly fix a lot of these issues.
![Uninstall](https://github.com/HugoJrH/HugoJrH/assets/126385725/fa2c8757-475f-462d-bcd9-66208be280ba)


To remediate the Windows vulnerabilities, I choose to update Windows. This version is old so it takes a few restarts to get it up to date.

![UPDATE COMPLETE](https://github.com/HugoJrH/HugoJrH/assets/126385725/0104aa37-afdd-4ca1-8fe6-ccabcaa6472d)

Here is a final comparison between the four scans I took while doing this lab. The last picture is the after remediation scan. There we can see a lot of the vulnerabilities that were being alerted are gone! Still a 1 critical but I'll remediate that another time!

![DONE](https://github.com/HugoJrH/HugoJrH/assets/126385725/90595c7f-3dcd-411b-b656-6f54e551290c)
