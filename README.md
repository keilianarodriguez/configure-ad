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

Step 1:
  
  I created the Domain Controller VM named "DC-1" with Windows Server 2022. I took note of the Resource Group and Virtual Network (Vnet) generated during this step, and I ensured that the Domain Controller's NIC Private IP address was set to static for stability. 

<p>
<img src="https://i.imgur.com/0rnWYGE.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/r5OcCH1.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>

Step 2: 
 I created the Client VM named "Client-1" using Windows 10, utilizing the same Resource Group and Vnet, and I confirmed that both VMs resided within the same Vnet for communication.

<br />

<p>
 Step 3: 
  I logged into Client-1 using Remote Desktop and initiated a perpetual ping to DC-1's private IP address with the command "ping -t <ip address>". Then, I logged into the Domain Controller and enabled ICMPv4 in the local Windows Firewall. Afterward, I checked back at Client-1 to confirm that the ping succeeded.
</p>
<br />

<p>
<img src="https://imgur.com/KokXxUm.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> <img src="https://imgur.com/zZIPYun.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> <img src="https://imgur.com/5ocwFE4.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> 
</p>
<p>
Step 4: 
  I logged into DC-1 and installed Active Directory Domain Services. Then, I promoted it as a Domain Controller, setting up a new forest named "domain.com". After restarting, I logged back into DC-1 as the user "domain.com\login".
  <p>
<img src="https://i.imgur.com/4GvpHpp.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> <img src="https://imgur.com/3hgLuj1.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> 
</p>


Step 5: 
In Active Directory Users and Computers (ADUC), I created two Organizational Units (OUs) named "_EMPLOYEES" and "_ADMINS". 
 <p>
<img src="https://i.imgur.com/D6ttTzJ.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
</p>


Step 6: 
Then, I added a new employee named "Jane Doe" with the username "janedoe" and assigned her to the "Domain Admins" Security Group. After logging out and closing the Remote Desktop connection to DC-1, I logged back in as "domain.com\janedoe" and continued using "janedoe" as the admin account.

 <p>
<img src="https://imgur.com/dLXASw6.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> <img src="https://imgur.com/WE4pX13.png" height="50%" width="50%" alt="Disk Sanitization Steps"/> <img src="https://imgur.com/6vWQ3oM.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>

Step 7: 
From the Azure Portal, I configured Client-1's DNS settings to point to the DC's Private IP address. Afterward, I restarted Client-1 from the Azure Portal.

<p>
<img src="https://imgur.com/BSsgNGG.png" height="70%" width="70%" alt="Disk Sanitization Steps"/> 
</p>

Step 8: 
I logged into Client-1 via Remote Desktop as the original local admin (login) and joined it to the domain, resulting in a computer restart. Upon logging into the Domain Controller via Remote Desktop, I verified that Client-1 appeared in Active Directory Users and Computers (ADUC) within the "Computers" container at the root of the domain. Finally, I created a new OU named "_CLIENTS" and moved Client-1 into it.

Step 9: 
I logged into Client-1 as "mydomain.com\janedoe" and accessed system properties. From there, I clicked on "Remote Desktop" and allowed "domain users" access to remote desktop. This enables non-administrative users to log into Client-1. Typically, this process would be handled using Group Policy to change settings across multiple systems simultaneously, which could be explored in a future lab.

<p>
<img src="https://imgur.com/rk7MZyl.png" height="70%" width="70%" alt="Disk Sanitization Steps"/> 
</p>


Step 10: 
I logged into DC-1 as "jane_admin" and opened PowerShell_ise as an administrator.

<img src="https://imgur.com/LPJWxHi.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>

Then, I created a new file and pasted the contents of the script from the provided GitHub link into it. After running the script and observing the accounts being created, I opened Active Directory Users and Computers (ADUC) to verify the accounts were in the appropriate OU. 

<p>
<img src="https://imgur.com/TUJ6gHN.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> <img src="https://imgur.com/t7Hygun.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
 
  
  Lastly, I attempted to log into Client-1 with one of the accounts created by the script, taking note of the password specified in the script.
  
  <img src="https://imgur.com/0jxeYCn.png" height="70%" width="70%" alt="Disk Sanitization Steps"/> 
</p>

