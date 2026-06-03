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

- <b>Windows 11</b>

- <b>Windows Server 2025</b>

<h2>Project walk-through:</h2>

<p align="center">
Network Diagram Reference: <br/>
<img src="https://github.com/brianspells00/Homelabsetup/blob/main/Network-diagram-ss.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
  <img src="[https://github.com/brianspells00/MSHomelabsetup/blob/main/11DomainServices.png](https://github.com/brianspells00/MSHomelabsetup/blob/main/13OrgUnit.png)" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
