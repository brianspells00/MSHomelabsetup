<h1>Windows Active Directoy</h1>


<h2>Description</h2>
This project consists of a Windows Active Directory creation and configuration. I walk through how I set up two virtual environments and how I configured them to communicate via an internal network that I set up. 
<br />


<h2>Languages, Utilities and Services Used</h2>

- <b>PowerShell</b> 
- <b>DNS Server</b>
- <b>Oracle VirtualBox</b> 
- <b>DHCP</b>
- <b>Remote Access</b> 
- <b>NAT</b>

<h2>Virtual Environments Used </h2>

- <b>Windows 10</b>

- <b>Windows Server 2025</b>

<h2>Project walk-through:</h2>

<p align="center">
Network Diagram Reference: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/Network%20Diagram.png"/>
<br />

<p align="center">
I started off by downloading the Virtual box package that aligned with your OS along with the Virtual Box extension pack. I chose VirtualBox because it is open source and can easily be scaled from personal to enterprise usage. Most importantly it allows you to run multiple VMs at once that have different operating systems: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/2VM%20download%20SS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
I then downloaded the latest version of Windows available along with Windows server 2025. Having the latest version ensures that previously found vulnerabilities are patched and cannot be exploited: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/3Windowsversions.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
I created the first VM(Domain Controller) and gave the VM 2 GB of RAM, 4 Processors and 50 GB of disk space: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/4VM%20Config.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
I changed the “Shared Clipboard” and “Drag-and-Drop” settings of the VM to “Bidirectional” so that I could easily input files from my host computer into the VM: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/5VM%20Config.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
I then added a second adapter configuration for the internal network: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/6VM1-internal-adapter2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
Now with the VM configured I can proceed with launching it and selecting the Windows Server 2025 file that I previously downloaded to be able to run Windows Server 2025 on the VM. While configuring the OS I selected Standard Evaluation (Desktop Experience) as the non-Desktop Experience options would use CLI for traversal. Then started the install and reboot process. : <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/7VMOS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
After the installation I created a strong password for the admin account. Then I was presented with the Windows login screen in which I used the password I created to login: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/8VM1AdminPassword.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/9VMOSlogin.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
Now that I’m in the OS of the VM I’ll be configuring the IP address. I configured the internal IP address in accordance with the network diagram. With the IP address set as 172.16.0.1
and the Subnet mask set as 255.255.255.0. I left the default gateway unfiled as the Domain Controller will be the gateway. As for the preferred DNS server the server will be using itself as the DNS which is why I used the IP address 172.16.0.1. I also took the liberty of renaming the PC to make later configurations easier: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/10IPsubnetconfig.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
For installing the Active Directory Domain Services I navigated through the “add roles and feature” tab in the server manager and selected my home server to install it on. I then toggled “Active Directory Domain Services” and continued to the install screen and began the install: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/11DomainServices.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
Once the services were installed I then navigated to the deployment configuration and selected “Add a new forest” and named my domain “personaldomain.com” . I finished the download and rebooted the system. Once it came back online I observed that the welcome screen was changed to “PersonalDomain\Administrator” and logged in. I wanted to create a dedicated domain admin account rather than the default admin account: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/12Adminacct.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/13OrgUnit.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
I navigated to the “Active Directory Users and Computers” program and ran it. While inside I selected my “personaldomain.com” and created an organizational Unit(OU) labeled “ADMINS”. Inside of the “ADMINS” OU I created a new user with my name and created a password. I was presented with multiple toggle boxes in relation to the password including: “User must change password at next logon” which if I was creating an account for another user to have admin access I would toggle on, “User cannot change password” which I would toggle on if I didn’t want a user to manipulate the login information, “Password never expires” which I would toggle off to add an additional layer of security to enforce a password policy, and “Account is disabled” which I would toggle on if I wanted to revoke the accounts access privileges: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/14Adminadded.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/15DomainAdmin.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
After I created the account I added the account as a Admin account as a member of “Domain Admins”. I signed out of the Microsoft account and used the credentials of the Admin username and password to sign in using the other user account. Once I confirmed that the sign in was successful I proceeded to configure RAS/NAT on the Domain controller so that the second VM I set up can access the internet through the Domain Controller while still being on its own private network: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/16Adminsignin.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
To do that I clicked on the “add roles and feature” tab in the server manager and in the “Server Roles” tab I toggled on “Remote Access” and in Server Services I toggled on “Routing”. Once the new role finished installing I clicked the “tools” tab on the top right and selected “Routing and Remote Access” and right-clicked the Domain Controller and selected “Configure and enable”. Once I clicked the next button I selected NAT as my configuration option and selected my home network. With the RAS/NAT configured I moved onto the next portion of configuring the Domain Controller which is installing the DHCP and defining the scope of the DHCP: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/17RemoteAccess.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/18RemoteRouting.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/19NATconfig.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
I clicked on the “add roles and feature” tab in the server manager and in the “Server Roles” tab I toggled on “DHCP”. Once it completed the download I clicked the “tools” tab on the top right and selected “DHCP" in the drop down box of my domain controller I right clicked the IPv4 option and selected “new scope”. I named the scope “172.16.0.100-200” and clicked next. I then used “172.16.0.100” as the start IP address, “172.16.0.200” as the end IP address and 255.255.255.0 as the Subnet mask. After continuing I was presented with an exclusions and delay page which I didn’t utilize but I did use the following Lease duration page which allowed me to customize how long a particular device can have an IP address. Since the primary use of the service will be on my desktop I set it to a higher day duration. If there was a lot of network traffic from many different devices I would set the lease to a shorter time so that the available IP addresses can be reused quicker: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/20DHCPinstall.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/21IPRange.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
After the lease page there was a Configure DHCP Options page which I toggles yes so that I could tell the client which servers to use for connecting to the internet through the gateway in which I used the internal NIC of “172.16.0.1” I then activated the scope. Which I confirmed was operational via the green check marks that previously were red: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/22Scopeoperational.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
Now that I’ve completed the configuration of the Domain Controller I wanted to add users to the directory using powershell. I downloaded a .txt file that contained 600 first and last names to which I added my first and last name. There’s a few ways to add the names into the active directory and they are situational. If I wanted to onboard a new employee I would simply create a new user and ensure they had the proper access based on their role. Since I’m adding a batch of names, using a script is more time efficient. I then defined what the script should/will be doing: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/23Powershell%20Script.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/24Define%20what%20the%20script%20does.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
I’m using Windows PowerShell ISE to be able to run the appropriate script to add the users. I downloaded the script from the same folder in which the .txt file was located. Upon running the script I was met with an error message that indicated my inability to run the script since the file was unable to be found. Using the pathing of the error code I placed the file in the appropriate spot and ran the code again. Once the script ran, it began to populate the usernames in Powershell in the first initial and lastname format that I requested: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/25Script%20denied.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/26Scriptsuccessful.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
The same thing could be accomplished by navigating the directory in which the file was originally. By using the cd command which changed which directory you’re in. For example the command cd C:\users\a-bspells\desktop\AD_PS-master would place me in the exact directory. Commands such as ls, pwd, can be used to find the directory if you’re unsure where you need to navigate to find the .txt file with the list of users.To confirm the entire script worked I navigated to the Active Directory Users and Computers application. I saw that a new OU was made under the name _USERS and verified that it contained each user that was in the .txt file: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/27confirmed%20the%20script%20worked.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
Now that the Domain controller is completely configured I’m creating the client VM. I named the new VM “Client 1” and gave it 4 processors, 4 GB of RAM and enabled Windows 10 as the OS. I also edited the settings of the VM to ensure bidirectional drag-and-drop and Shared Clipboard. I then changed the network adapter settings so that the Client 1 VM will be connected to the internal network: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/28VM2%20network%20config.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
I ran the Client VM and selected the Windows 10 disk download file from the Microsoft Website, installed it onto the VM and let the system reboot. Once I logged into the account I went to settings and verified that the Client was connected to the internal network “personaldomain.com” I also opened the Windows Command Prompt and ran the prompt [> ping personaldomain.com]  to communicate with the domain controller and got response which indicates connectivity: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/29Client%20is%20connected%20to%20the%20DC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/30cmdPing.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p align="center">
Since my machine is running Windows 10 home edition I’m unable to place the computer into the Active directory. If I were to be running an enterprise version of Windows 10 then I would be able to see the Client 1 in the Computers directory of the Active Directory Users and Computers application. I then went to the DHCP server in the Domain Controller and saw that the DHCP gave the Client 1 VM and IP address of 172.16.0.101. On an enterprise level every device added would be assigned an IP address from 172.16.0.101-200. Since there is an expiration time on the IP lease that would allow IP addresses to be reused: <br/>
<img src="https://github.com/brianspells00/MSHomelabsetup/blob/main/31Client%20computer%20assigned%20an%20IP%20address.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<h2>Conclusion:</h2>
I previously understood that Windows Active Directories are used to manage users, user permissions, computers, security policies, and network resources. After finishing configuring my Active directory. I learned and received a deeper understanding of how to configure a domain, manage users within the domain. I also learned how to utilize Organizational Units to arrange and classify users, admins and computers. This lab also allowed me to get experience in DNS, DHCP, NAT/NAS services/configuration. The utilization of Powershell was also very insightful on how I could take a tedious task and have it automated for an efficient workflow.
