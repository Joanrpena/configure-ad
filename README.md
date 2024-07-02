<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory within Azure</h1>
This lab will serve as a follow-up to the previous lab where I set up a VM as a domain controller and installed Active Directory. In this lab I will be configuring Active Directory, join a client machine into the domain, and create user accounts.
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (22H2)

<h2>Configuration Steps</h2>

<p align="center">
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/c643917b-34e0-49d2-879a-3bba5db6c4d3" height="60%" width="60%" alt="Configuration Steps" />
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/350f4ec6-3e5e-4fb4-931d-f0061c48b03d" height="60%" width="60%" alt="Configuration Steps" />
   <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/f4e3b157-78d6-48a9-8d60-857a890d34c4" height="60%" width="60%" alt="Configuration Steps" />
</p>

- Now that we have successfully installed Active Directory on our Domain Controller(DC) VM, we can start configuring Organizational Units(OU) and Users. We'll start creating an OU On the top right of server manager click on Tools, then click on Active Directory Users and Computers to open the Active Directory window. On the left hand side you should see the domain you created, with a series of default files included inside of it. Right click on your domain > Navigate to New > Click Organizational Unit > For this lab we'll create two OUs one named "_EMPLOYEES" and another named "_ADMINS". Now we will create a User with Administrator privileges. Click on your _ADMINS folder > Right click the empty space > New > User (Avoid using a generic name such as "admin" or "user" to simulate best practices. A new user will almost always be created with a real name) for this lab we'll use "John Smith". > Fill out the first and last name information, for this lab the logon name will be john_admin > Click Next > Set a password (For this lab we will set the password to never expire, and to not reset at logon. In general this is bad practice, so keep this in mind.) > Next > Finish. We will now set admin priveledge to our created User. Right click the User > Click Properties > Member Of > You can type Domain to get a view of all the default groups, but for this step we will use "Domain Admins" > OK. Now we can log out of our default account and log in to the newly created user account to test if everything works properly using the credentials for your domain. Example: "joandctest.com\john_admin"
<br />

<p align="center">
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/2ea0509d-9920-44e9-beea-315435445b32" height="60%" width="60%" alt="Configuration Steps" />
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/6e4c7899-c531-4fe5-b0b3-7680b733a04d" height="60%" width="60%" alt="Configuration Steps" />
</p>

- Now that we've created our OUs and an Administrator User we can joint our client VM to the domain, but before we do that it's important to configure the DNS settings beforehand. The client VM's DNS settings have to be set to the private static IP Address of our Domain Controller. To do this, on Azure click on your client VM > On the left hand side click "Network Settings" > Click on your Virtual NIC > on the left hand side click DNS Servers > Under DNS Servers click Custom and Paste your DC VM's private IP Address > Press Save. If your client VM is running on Azure go ahead and restart it for changes to take effect.
<br />

<p align="center">
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/8a2e58a7-3d5a-4912-978f-69bae04aec3e" height="60%" width="60%" alt="Configuration Steps" />
   <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/0788c10a-4aac-40ad-b2d6-8be0ef9aa821" height="60%" width="60%" alt="Configuration Steps" />
</p>

- To join our client VM to the domain establish a connection to it and log in as the original local admin > right click on the Start icon, then click System > Rename this PC (Advanced) > Change > under Member Of click Domain and enter the name of the domain you created previously (joandctest.com) > Enter the credentials for the admin user you created earlier. EX: (joandctest.com\john_admin) > Restart the VM. Log back in to your DC VM and confirm the client VM appears in the Active Directory Users and Computers panel.
  <br />

<p align="center">
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/7daf0b31-8cf7-4339-aeca-2c49e25d8dd4" height="60%" width="60%" alt="Configuration Steps" />
 
</p>

- We will now enable up Remote Dekstop for non-administrative users, so that users in the domain can access the client computer. Log in to your client VM with your administrator account > Right click the Start icon and click System > Remote Desktop > Select users that can remotely access this PC > Add > type Domain Users and click check names (this makes it so that every user thats part of the Domain Users group has access) > OK. You can now log into the client VM as a normal, non-administrative user.
  <br />

  <p align="center">
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/99431c4c-2a7f-4f1e-809c-3d4a510b1e7f" height="60%" width="60%" alt="Configuration Steps" />
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/68bd14c2-116b-428e-99d3-838e43653fd0" height="60%" width="60%" alt="Configuration Steps" />
 
</p>

- Next, we'll create Users. You can do this manually and assign each user their permissions, but for this lab I'll be using a PowerShell script to automate this process. You can find the script <a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1">Here.</a> Log in to your Domain Controller VM, we'll need the Active Directory modules for this step. On the lower hand search bar type Powershell_ise > Right click and open PowerShell ISE as Administator > copy the contents of the script onto the editor, then run the script and observe the User accounts being created. The script is set to create 10,000 random Users, stop the script when you feel comfortable.
  <br />
  
   
