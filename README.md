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
- Creating Domain
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

![Screenshot 2023-03-18 183546](https://github.com/Kobla2020/configure-ad/assets/127445078/c922903e-82ae-4ce4-a451-0a6bac01d5c0)
</p>
<p>
Next you need to test the connection between DC-1 and Client-1. So after setting DC-1s private IP to static, sign in to remote desktop on Client-1. Remember to type in the credientials you made during your Client-1 VM creation. After signing in to Client-1, go to the search bar at the bottom and type "cmd" to access Client-1s command line. now you want to test Client-1s connection to DC-1 so we need to "Ping" DC-1s private IP which, for me is 10.0.0.4. So after intially pinging DC-1s private IP it should have a prompt that reads "request timed out" this means that something is blocking Client-1 from pinging DC-1s private IP so now we need to unblock that and we also want to confirm  that we unblocked it via command line. To do this ping DC-1s private IP address and then type "-t" to get a reccuring ping. After doing this, sign into DC-1 using remote desktop. After signing in, type "Firewall" in the search bar and click on "Windows Defender Firewall with Advanced Security" app. After opening up windows defender firewall, it should give you some options on the left hand side, click where it says "inbound rules" then it should redirect you to a new page within the app that has all the inbound rules. You should see some columns starting with the titles at the top of each column reading: name, group, profile, etc. Go over until you see the column titled "protocol" and then click on "protocol" and now it should arrange everything in the order of protocols. After seeing this, go down to the "ICMPV4" protocol and back over to the "names" column and make sure that the first three in the "ICMPV4" protocol are enabled. To enable a rule, go to the far right and underneath "core networking diagnosis", should give you the option to enable thesse rules. After enabling the rules, go back to Client-1s VM and notice that now you are successfully pinging DC-1.
</p>
<br />

![Screenshot 2023-03-19 011333](https://github.com/Kobla2020/configure-ad/assets/127445078/1fb9fe5b-f8e3-45ef-b4f8-d361f6ce3168)

</p>
<p>
Now we're going to install active Directory on DC-1. If its not open already, open DC-1 and go into the server manager. The server manager should automatically pop up when you open DC-1 but just in case it doesnt, type "Server Manager" in the Windows search bar at the bottom of the desktop. After opening server manager, click on the option that says "add roles and features". After clicking on add roles and features, keep clicking next until you get to the page where there are multiple options that you can click to fill in the box. Click on the option that says "Active Directory and Domain Services" then after clicking next, it should take you to a page where it just confirms whether or not to add the feature, on that page click "add feature". After adding active directory and domain services, click next until you can not click next anymore and when that happens, it should just give you the option to install. After installing active directory and domain services, in the upper right hand corner next to "manage" there should be a flag and right next to that flag is a triangle with an exclamation point in the middle, click on that and we'll continue on to making our domain.
</p>
<br />

![Screenshot 2023-03-19 014121](https://github.com/Kobla2020/configure-ad/assets/127445078/87b90925-6266-42ed-942a-341b4167aa1d)
</p>
<p>
After clicking on the flag icon, we need to make a domain. You can type in any name, just make sure it ends with ".com". For this example, I used "activedirectory.com". After deciding on the name, click next and enter any password into the bar. Now we can just click next until it gives us the option to install and upon installing, it should restart our DC-1 VM and now we should be able to use our domain to log into DC-1 as seen in the picture.
</p>
<br />

![Screenshot 2023-03-19 015711](https://github.com/Kobla2020/configure-ad/assets/127445078/03a392ee-acea-4d4c-839f-f9977d87df5d)
</p>
<p>
 Next we need to make our admin user inside of DC-1. After logging back into DC-1, open the server manager and in the top right hand corner next to manage, says tools. Click on tools and then click on "Active Directory Users and Computers" which should be the fifth option from the top. After opening up active directory users and computers, you should be able to see your domain with an expand arrow to the right of it. Click where you see your domain and then observe the options starting with "Builtin" and ending with "Users" we are not going to do anything with those for now, instead, right click the open space below "users" go to "new" then click on "organizational unit" which should be the fourth option from the bottom. We are going to make two organizational units. One named "_EMPLOYEES" and another named "_ADMINS". After making these two organizational units, click on your "Admins" organizational unit and inside should be empty, right click the empty space and click "new" then click "user" which should be the second option from the bottom. You can type in any name you would like. After choosing your name, type the name in however way you would want to use it to sign in. The example I used was my own name "Kordell Blake" and the logon info I used was "kordell.blake". When you click next, you can use any password you would like, just be sure to remember the password and uncheck the box where it says "user must change password at next log in" and check the box where it says "password never expires". After making your password, click next and you should have your admin. Now we need to add your user you just made to the "domian admins" group. Right click on the account you just made and go to "Properties" and after going to properties, you should see some tabs you can click on. Go to the tab that says "member of" which should be in the top left hand corner. After clicking on member of, you should see an option that says "add". after clicking add, in the box at the bottom, type: "Domain Admins" next you press "Ok" then "Apply". Now we have our domain admin that is now part of the domain admin group! Log out of DC-1 and log back in using the log in name you made along with your domain plus the password that you also made.
</p>
<br />

![Screenshot 2023-05-02 174626](https://github.com/Kobla2020/configure-ad/assets/127445078/bb882767-b378-488e-8808-7909659e7f15)
</p>
<p>
The next step is connecting our Domain to Client-1. If you are not logged in already, log into your Client-1 VM. Once you are logged in, right click your windows icon on your windows desktop and click on the option where it says "System". Now a new window should have popped up and on the right hand side, it should have some options that are considered to be "related settings", click on the last one that says "Rename this PC(Advanced)". After clicking on rename this PC, a new, smaller window should pop up with some tabs on the top. the first tab reads "Computer Name" and has two option you can click on: "Network ID" and "Change". Click on the option that says "Change" and after doing this, at the bottom of the new window, it says "Member of" and gives you two more options, click on domain and type in your domain name that you made. So after typing in your domain name, and pressing "OK" you should recieve an error that basically says your Client-1 VM is not connected to that domain. In order to connect your domain to your Client-1 VM, we need to go back in to the azure portal. Next click on your Client-1 VM and Now we just pretty much follow the same steps we used to change our DC-1 VM Private IP to static except for a few changes. In the list of options, click on "networking" then click on your network interface which should be: "client-1849" or some other random numbers. After clicking on your network interface, instead of clicking on to IP configurations, we are going to click on "DNS servers" and where it says "DNS servers" and right below that it gives you two options: "inhereit from virtual network" or "Custom". click on custom and type in DC-1s private IP address and then click save at the top. In order to fully register these changes, we need to restart our Client-1 VM. So in the azure portal, go back to your Client-1 VM, click on it and at the top, it will give you the option to restart your Client-1 VM. After your VM is restarted, relog back in to Client-1 and follow the same steps from earlier, you should be able to connect your domain to your Client-1 VM.
</p>
<br />

![Screenshot 2023-03-19 032529](https://github.com/Kobla2020/configure-ad/assets/127445078/242cbdc5-b2a1-4d25-a7a2-3465adbb5754)
</p>
<p>
This picture illustrates that I can now sign in to both DC-1 and Client-1 as my user, the domain admin.
</p>
<br />

![Screenshot 2023-03-19 033156](https://github.com/Kobla2020/configure-ad/assets/127445078/8e2974ec-b3b7-414c-bb2f-75d765492bf9)
</p>
<p>
Next is setting up remote desktop for non-administrative users in Client-1. Sign in to Client-1 as the domain admin(it may take a little while). After signing in, right click the windows icon and click on "System" again. Now under "Related settings" click on "Remote Desktop" which should be the third option down. After clicking on remote desktop, click on "Select users that can remotely access this PC" which will be at the bottom under "User Accounts". This should open a mini window. Click on "Add" and type "Domain Users" in the box and click "OK".
</p>
<br />

![Screenshot 2023-03-19 035134](https://github.com/Kobla2020/configure-ad/assets/127445078/9953991a-b508-460a-a3f2-8d9a1543d869)
</p>
<p>
This is the last step as well as an exercise. After setting up remote desktop for non-administrative users in Client-1, I went back in to DC-1 and opened Powershell_ise as an administrator. To do this, type powershell_ise in the desktop search bar and right click the powershell_ise app. I then ran a script where 10000 random users were made, then I reopened active directory users and computers and clicked on "Employees" and now inside of the employees organizational unit, are those 10000 users. After observing the users being made I right clicked on one of the users and clicked on properties and went to the "account" tab and entered in the log in information of the user I chose which was: "beve.bawi".
</p>
<br />

<p>
<img src="https://i.imgur.com/wOXvySW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After joining my user to my domain I logged out of Client-1 and logged back in as one of the 10000 random users.
