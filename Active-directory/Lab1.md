---
layout: post
title: "Active Directory Lab - Part 1: Server Prep & Domain Setup"
date: 2025-07-05
categories: lab ad-ds windows-server
---

In this lab, we’re setting up a Windows Server as a fully functional Domain Controller using Active Directory Domain Services (AD DS). This is the foundation of any enterprise IT infrastructure.  
you can do this lab in VirtualBox like I did, or choose to run it on any cloud provider such as Azure, AWS, or Google Cloud.  

This is Part 1 of a multi-part Active Directory lab series designed to simulate a real-world environment. We’ll move step-by-step from initial setup to deploying users, policies, and securing a domain.

## 1. Change Server Name

After the instalation of the Server on VirtualBox. then we can change the Server name for more clarity and easy reference:

- Open Server Manager (it opens by default), Go to Local Server (left-hand menu). Click on the current computer name  
- I Changed mine to `HC1` for easy reference in the next labs. 
![rename server ](/Uploads/Images/1.PNG)
![ok](/Uploads/Images/2.PNG)

then click OK and restart the server


## 2. Set Static IP Address

We have to set a static IP address for the server in order to make it reliable, reachable, and consistent on the network.

![Set static IP placeholder](/Uploads/Images/3.PNG)

## 3. Install Active Directory Domain Services

### 3.1 Add AD DS Role

without the AD DS role, your server is just like any other server, to turn it into a domain controller it needs AD DS role (think of it like installing the engine into the car before you can derive(create users, manage domains, set up group policies…))  
Adding the AD DS role is the first and essential step in making your server a Domain Controller. Without it, you cannot create a domain, join machines to it, or manage users centrally  
here are the steps to do that:
Open Server Manager then Click Manage → Add Roles and Features. 
![Roles and Features](/Uploads/Images/4.PNG)

Click Next through the first few steps until you reach Server Roles.
Check the box:Active Directory Domain Services
![Check the box](/Uploads/Images/5.PNG)

A pop-up will appear → Click Add Features.
![popup](/Uploads/Images/6.PNG)

Click Next until you reach Install, then click Install.
![Install](/Uploads/Images/7.PNG)
Wait for installation to finish
![Install](/Uploads/Images/8.PNG)
Installation is now finished.
![Install](/Uploads/Images/9.PNG)

### 3.2 Promote the Server to Domain Controller

after adding the AD DS Role, our server is ready to become a domain controller but not one yet, that is why we have to promote it to become one,when we promote it we are : 
- Creating a new domain or joining an existing one.
- Installing the AD database.
- Setting up the SYSVOL and NTDS folders.
- Activating the server as the controller for the domain. 

after the promotion, we have a domain controller that is able to handle :  
- Authorization (what they can access)
- Directory Services (users, computers, groups, etc.)
- Group Policies (security and configuration enforcement) and DNS integration.  

Here are the steps to do it:

1. Open **Server Manager**  
   Click the yellow ⚠ warning flag and choose:  "Promote this server to a domain controller"

![Promotion warning flag placeholder](/Uploads/Images/10.PNG)

2. **Deployment Configuration**  
- Select: **Add a new forest**
- Root domain name: `Hlab.local`
- Click Next
![Deploy conf](/Uploads/Images/11.PNG)

3. **Domain Controller Options**  
- ✅ Domain Name System (DNS)
- ✅ Global Catalog (GC)
- ❌ Read-only domain controller (RODC)
- Set a DSRM password
- Click Next
![Options](/Uploads/Images/12.PNG)

4. **DNS Options**  
- Ignore delegation warnings this is normal for the first DC
- Click Next
![Options ignore](/Uploads/Images/13.PNG)

5. **NetBIOS Name**  
- Accept default
- Click Next
![Netbios](/Uploads/Images/14.PNG)

6. **Paths**  
Unless you have a specific reason, leave the default paths:  
- Database: `C:\Windows\NTDS`
- Logs: `C:\Windows\NTDS`
- SYSVOL: `C:\Windows\SYSVOL`
- Click Next
![Paths](/Uploads/Images/15.PNG)

7. **Review Options**  
- Confirm settings
- Click View script if you want to save the PowerShell equivalent
- Click Next
![Paths](/Uploads/Images/16.PNG)


8. **Prerequisites Check**
   - Wait for the check to complete
   - Minor warnings are fine
   - Click Install
![chwck](/Uploads/Images/17.PNG)
![chwck](/Uploads/Images/19.PNG)

The server will automatically reboot after installation.
![reboot](/Uploads/Images/20.PNG)


---

## Domain Controller Is Ready

we now have a fully functional Domain Controller!

- Domain: `Hlab.local`
- Services: AD DS, DNS
![DC Ready](/Uploads/Images/21.PNG)
![DC Ready](/Uploads/Images/22.PNG)

### [Next on Part 2:]({% link _posts/2025-07-06-ADLABP2.markdown %})
- Create OUs (Organizational Units)
- Add users and groups