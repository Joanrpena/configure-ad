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
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/c643917b-34e0-49d2-879a-3bba5db6c4d3" height="60%" width="60%" alt="Installation Steps" />
  <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/350f4ec6-3e5e-4fb4-931d-f0061c48b03d" height="60%" width="60%" alt="Installation Steps" />
   <img src="https://github.com/Joanrpena/configure-ad/assets/131486928/f4e3b157-78d6-48a9-8d60-857a890d34c4" height="60%" width="60%" alt="Installation Steps" />
</p>

- Now that we have successfully installed Active Directory on our Domain Controller(DC) VM, we can start configuring Organizational Units(OU) and Users. We'll start creating an OU On the top right of server manager click on Tools, then click on Active Directory Users and Computers to open the Active Directory window. On the left hand side you should see the domain you created, with a series of default files included inside of it. Right click on your domain > Navigate to New > Click Organizational Unit > For this lab we'll create two OUs one named "_EMPLOYEES" and another named "_ADMINS". Now we will create a User with Administrator privileges. Click on your _ADMINS folder > Right click the empty space > New > User (Avoid using a generic name such as "admin" or "user" to simulate best practices. A new user will almost always be created with a real name) for this lab we'll use "John Smith". > Fill out the first and last name information, for this lab the logon name will be john_admin > Click Next > Set a password (For this lab we will set the password to never expire, and to not reset at logon. In general this is bad practice, so keep this in mind.) > Next > Finish. We will now set admin priveledge to our created User. Right click the User > Click Properties > Member Of > You can type Domain to get a view of all the default groups, but for this step we will use "Domain Admins" > OK. Now we can log out of our default account and log in to the newly created user account to test if everything works properly using the credentials for your domain. Example: "joandctest.com\john_admin"
 <br />
