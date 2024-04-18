<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High Level Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/0rnWYGE.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/r5OcCH1.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1:
  
  I created the Domain Controller VM named "DC-1" with Windows Server 2022. I took note of the Resource Group and Virtual Network (Vnet) generated during this step, and I ensured that the Domain Controller's NIC Private IP address was set to static for stability. 


Step 2: 
 I created the Client VM named "Client-1" using Windows 10, utilizing the same Resource Group and Vnet, and I confirmed that both VMs resided within the same Vnet for communication.
 
</p>
<br />

<p>
<img src="https://imgur.com/KokXxUm.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> <img src="https://imgur.com/zZIPYun.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> <img src="https://imgur.com/5ocwFE4.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> 
</p>
<p>
Step 3: 
  I logged into Client-1 using Remote Desktop and initiated a perpetual ping to DC-1's private IP address with the command "ping -t <ip address>". Then, I logged into the Domain Controller and enabled ICMPv4 in the local Windows Firewall. Afterward, I checked back at Client-1 to confirm that the ping succeeded.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
