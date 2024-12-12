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

- Setup Domain Controller and Clinet-1 server in Azure
- Install Active Directory
- Create Domain Amdin user within the domain

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


