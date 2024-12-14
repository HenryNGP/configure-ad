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

- Setup Domain Controller and Client-1 server in Azure
- Install Active Directory
- Create Domain Admin user within the domain
- Join Client-1 to domain
- Setup Remote Desktop for non-administrative user on Client-1

<h2>Deployment and Configuration Steps</h2>

<p>
First create a resource group in Microsoft Azure
<p></p>
<img width="386" alt="image" src="https://github.com/user-attachments/assets/4a5fce3a-446c-4b32-87fe-a7bd7470ef48" />
</p>
Create a Virtual Network and put in the resource group you just created.
</p>
<img width="594" alt="image" src="https://github.com/user-attachments/assets/da39564e-e83c-45bd-9659-63b3f314b57b" />
</p>
Now create a new virtual machines dc-1 and client-1. REMEMBER: dc-1 and client-1 virtual machines need to be same region as Virtual Network, my case is Central US. Note: for dc-1 image need to be Window Server 2022, and client-1 is Window 10. Also create a username and password.
</p>
<img width="716" alt="image" src="https://github.com/user-attachments/assets/f71cad01-6479-4932-b5aa-cf324817c8cf" />
</p>
<img width="689" alt="image" src="https://github.com/user-attachments/assets/0f36ae14-d3e5-44b0-8f8b-ed249866c2bf" />
</p>
After created both virtual machine we need to configure IP address to be static for dc-1 and private IP address to client-1.
</p>
For dc-1, Click on dc-1 > Networking > ipconfig1 (primary). Then click on ipconfig then set to static and save. </p>
<img width="589" alt="image" src="https://github.com/user-attachments/assets/a8dae4a1-d417-4b93-b862-0d4abb98fa9c" />
<img width="1043" alt="image" src="https://github.com/user-attachments/assets/1d05f800-85f0-4c32-9a6e-06b65e57ebf9" />
</p>
For client-1, click on client-1 virtual machine > Networking > DNS servers and copy/paste the dc-1 private IP address and save. Then restart the client-1 in Azure.
</p>
<img width="572" alt="image" src="https://github.com/user-attachments/assets/a9652877-214f-45b7-ad90-c4afee3df2af" />
</p>
"Just for lab testing": Now login dc-1 using remote desktop connection and turn off the firewall by using a run program the type 'wf.msc' </p>
<img width="281" alt="image" src="https://github.com/user-attachments/assets/6cc392fc-7244-40b8-83cd-6ca1418adbeb" />
</p>
Click on Windows Defender Firewall Properties. All firewall need to be turn off: Doamin, Private, Public Profile. </p>
<img width="554" alt="image" src="https://github.com/user-attachments/assets/973bd1c4-f5c8-4e18-bb6e-903fc307a871" />
</p>
To ensure client-1 ping is on private IP address go to window powershell and type 'ping 10.0.0.4'
</p>
<img width="337" alt="image" src="https://github.com/user-attachments/assets/9263af4c-f2d7-4d0a-a2c5-c361d7153bd0" />
</p>
And check if client-1 is in private IP address or not type 'ipconfig /all'
</p>
<img width="533" alt="image" src="https://github.com/user-attachments/assets/792d340c-df05-41e3-9882-63968d97808b" />
</p>
To install active directory go to dc-1 and go to server manager, then 'add role and features' click next. Then on server roles check 'Active Directory Domain Services' box and install.
</p>
<img width="743" alt="image" src="https://github.com/user-attachments/assets/6599f2ed-9186-4a18-aa67-97251227872d" />
</p>
After install, we need to promote this server to a domain controller. By click on the flag icon then click on promote > Add a new forest > mydomain.com is what I am using. Uncheck DNS options, and install.
</p>
<img width="401" alt="image" src="https://github.com/user-attachments/assets/8371a901-acde-4adc-9cad-7745d228bbf7" />
</p>
<img width="575" alt="image" src="https://github.com/user-attachments/assets/9c2502fe-a0d8-4e6a-bddf-5e742369687f" />
</p>
After the install it will restart and now you need to login using mydomain\"your user" for username login in remote desktop connection. My case is mydomain\labuser.
</p>
<img width="313" alt="image" src="https://github.com/user-attachments/assets/8596d771-bf1a-4ad7-9e08-d283f3b682c8" />
</p>
To create an Admin user within the domain, first you need to create two oragnizational unit. By typing Active Directory User and Computers on window. Right click on mydomain.com > new > organization unit and name it _EMPLOYEES and _ADMINS.
</p>
<img width="560" alt="image" src="https://github.com/user-attachments/assets/c975e9a5-343f-4b11-b2d7-f2bbd407691a" />
</p>
<img width="365" alt="image" src="https://github.com/user-attachments/assets/efb1428c-9559-45fe-9bc2-c37ce0d17b2f" />
</p>
Create a new admin-user go to admin folder you just created then right click and new user.
</p>
<img width="560" alt="image" src="https://github.com/user-attachments/assets/ddd6beef-5470-4995-bfc1-578a1f764c94" />
</p>
After creating a user, you need to assgin user as admin by right click on the name then properties > Member of > adds > then type domain admins > check name. This user will become admin.
</p>
<img width="489" alt="image" src="https://github.com/user-attachments/assets/776a83a5-dc54-4085-a6b4-c8db8f6c318d" />
</p>
To login to admin account 'mydomain\'whateverusername_admin'. My is mydomain\tim_admin.
</p>
<img width="326" alt="image" src="https://github.com/user-attachments/assets/bb1ff41d-4c51-4233-a034-1b039c64fe51" />
</p>
Now to make client-1 server to login the domain we need to change some setting. Type 'About' in window > 
Rename > Change > Domain > type mydomain.com. The log in your admin account. Then it restart.
</p>
<img width="827" alt="image" src="https://github.com/user-attachments/assets/e7e8918b-a253-4f72-815c-0e3d5fe3c2df" />
</p>
<img width="346" alt="image" src="https://github.com/user-attachments/assets/4b839a4d-0b1f-41e4-ad5d-372abf28c1e7" />
</p>
To verify if client-1 is in a domain system. Check on Active directory users and computer > mydomain.com > Computer.
</p>
<img width="566" alt="image" src="https://github.com/user-attachments/assets/db9fb668-9b8b-40db-943c-8ee316f47c5f" />
</p>
To setup remote desktop for non-administrative users on client-1. You need to log in client-1 with admin account. Type "Remote Desktop setting" > 'Select users that can remotely acces this PC' > Add > type 'Domain users'. You can now log into Client-1 as a normal, non-administrative user now.
</p>
<img width="615" alt="image" src="https://github.com/user-attachments/assets/27645d4d-94f5-4c7b-81aa-d9ebeb902b1a" />
</p>
