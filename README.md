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

<h2>High-Level Deployment and Configuration Steps</h2>

- Setting up resources in Azure
- Ensuring connectivity between DC-1 and Client-1
- Installing Active Directory
- Creating Admin and Normal user accounts in Active Directory
- Joining Client-1 to your domain
- Setting up remote desktop for non-administrative users in Client-1
- Creating a bunch of additional users and attempt to log in to Client-1

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/8ulVfQK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The first thing you are going to want to do is create two virtual machines, one named "DC-1" and the other named "Client-1". Make sure the server that DC-1 is running on is "Windows 2022 datacenter" and for Client-1 its the normal "Windows 10". Next we have to set DC-1's private IP to static instead of dynamic. To set DC-1's private IP to static we have to first click on your DC-1 VM after it is done being made, then where you see all the options on the left hand side of your screen starting with "overview", go down until you see "networking" and click on that.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
