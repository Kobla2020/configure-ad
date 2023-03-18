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
The first thing you are going to want to do is create two virtual machines, one named "DC-1" and the other named "Client-1". Make sure the server that DC-1 is running on is "Windows 2022 datacenter" and for Client-1 its the normal "Windows 10". Next we have to set DC-1's private IP to static instead of dynamic. To set DC-1's private IP to static we have to first click on your DC-1 VM after it is done being made, then where you see all the options on the left hand side of your screen starting with "overview", go down until you see "networking" and click on that. Now right beside "network interface" you should see "dc-" then some random numbers, click on that and it should bring you to the network interface page for DC-1 and it should also give you another list of options. Go down until you see "IP configurations" and click on that. Now you should be able to see your only IP configuration which is ipconfig1, click on that and it should bring you to the final page where you can change your private IP to static. At the bottom it should give you the option whether or not you want your private IP on dynamic or static, it should be on dynamic as the default, change it to static and click on save at the top.
</p>
<br />

<p>
<img src="https://i.imgur.com/RbktFFb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next you need to test the connection between DC-1 and Client-1. So after setting DC-1s private IP to static, sign in to remote desktop on Client-1. Remember to type in the credientials you made during your Client-1 VM creation. After signing in to Client-1, go to the search bar at the bottom and type "cmd" to access Client-1s command line. now you want to test Client-1s connection to DC-1 so we need to "Ping" DC-1s private IP which, for me is 10.0.0.4. So after intially pinging DC-1s private IP it should have a prompt that reads "request timed out" this means that something is blocking Client-1 from pinging DC-1s private IP so now we need to unblock that and we also want to confirm  that we unblocked it via command line. To do this ping DC-1s private IP address and then type "-t" to get a reccuring ping. After doing this, sign into DC-1 using remote desktop. After signing in, type "Firewall" in the search bar and click on "Windows Defender Firewall with Advanced Security" app. After opening up windows defender firewall, it should give you some options on the left hand side, click where it says "inbound rules" then it should redirect you to a new page within the app that has all the inbound rules. You should see some columns starting with the titles at the top of each column reading: name, group, profile, etc. Go over until you see the column titled "protocol" and then click on "protocol" and now it should arrange everything in the order of protocols. After seeing this, go down to the "ICMPV4" protocol and back over to the "names" column make sure that the first three in the "ICMPV4" protocol are enabled. To enable a rule, go to the far right and underneath "core networking diagnosis", should give you the option to enable thesse rules. After enabling the rules, go back to Client-1s VM and notice that now you are successfully pinging DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
