# active-directory-<p align="center">
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

<h2>Step 1: Provision Azure Resources</h2>
<ul>
-First we create a resource group named Active-directory for future reference and we will also create a virtual machine, make sure the azure Virtual machine is set the resource group we just created. "Active-directory"

<img width="948" height="631" alt="Screenshot 2026-03-05 094917" src="https://github.com/user-attachments/assets/c480df36-c0a3-4a40-8b54-2db5850590a3" />

<img width="1066" height="768" alt="Screenshot 2026-03-05 095303" src="https://github.com/user-attachments/assets/edca337a-d8c7-4ee7-8a2e-8087c45c1a30" />


<img width="966" height="878" alt="trrrrr" src="https://github.com/user-attachments/assets/3632ef57-efe2-4a64-998c-01250713e160" />

- Create a Windows Server 2022 virtual machine to serve as the Domain Controller, and name it DC-1.
make sure to set the correct resourse group and region when creating the virtual machine.

<img width="1063" height="907" alt="activednewski" src="https://github.com/user-attachments/assets/df992425-34a9-453d-ad35-18b629dae5f8" />

Make sure to also set a safe username and password as well to able to login to our virtual machine and later install active directory to it, also be sure to put it in the virtual network we created.

<img width="1098" height="872" alt="nelliii" src="https://github.com/user-attachments/assets/14bae4fc-74a0-4523-9a09-224fee35a5a3" />

<img width="961" height="997" alt="vnet" src="https://github.com/user-attachments/assets/f5d39909-56ed-47c8-b17a-cb702052db00" />

- Create a Windows 11 virtual machine named Client-1 within the same Resource Group and VNet as DC-1

  <img width="1041" height="1007" alt="yujjjjjj" src="https://github.com/user-attachments/assets/683e132d-1ce1-4200-a71f-2dcf84d3b555" />


After our VM is created, set Domain Controller’s (dc-1) NIC Private IP address to be static
<img

<img width="965" height="1012" alt="image" src="https://github.com/user-attachments/assets/860a7dd0-e03d-4b63-9912-cb3d30a10a72" />

<img width="947" height="1015" alt="image" src="https://github.com/user-attachments/assets/5c2e7bb5-e923-485c-b2da-e3040153e45a" />

<img width="967" height="1007" alt="static" src="https://github.com/user-attachments/assets/029d745d-e64a-4c9b-8ed7-c8970f41f9cd" />

- next we will be logging into our virtual machine to (dc-1) using remote desktop connection this is the virtual machine we will be using as a domain controller we do that by taking the I.P adress from our azure portal then inputing the username and password we created earlier.

<img width="1877" height="607" alt="Screenshot 2026-07-13 112549" src="https://github.com/user-attachments/assets/7e95a0fa-ca14-4f35-bed5-919977a8ddf8" />

<img width="1517" height="845" alt="Screenshot 2026-07-13 112947" src="https://github.com/user-attachments/assets/0ec387dc-42d8-4706-b578-d2ca178eefce" />

<img width="687" height="536" alt="Screenshot 2026-07-13 113042" src="https://github.com/user-attachments/assets/9ffbb54e-d477-4ae2-8691-aa65d5fb6a34" />

 -Since its our first time logging in we will get this security prompt click yes and we will be connected to our domain controllers virtual machine (dc-1)
 
<img width="1576" height="1007" alt="Capture" src="https://github.com/user-attachments/assets/a551088b-220e-4eec-8712-ed306b0ea8c4" />

-We succesfully connected to our virtual machine now we will disable our windows firewall using the comman "wf.msc" we are disabling to be able to send out a virtual continous ping to ensure both our virtual machines are able to connect to eachother.

<img width="1404" height="1020" alt="Capture2" src="https://github.com/user-attachments/assets/b517c55b-0104-4abc-8224-03484c7a5bf8" />

<img width="680" height="671" alt="Capture3" src="https://github.com/user-attachments/assets/51e773c4-a7ba-4161-8bcb-5c5c65e04479" />

-the next step is too set Client-1’s DNS settings to DC-1’s Private IP address within our azure portal we go to client-1 NIC and paste dc-1 private address

<img width="1211" height="887" alt="dns" src="https://github.com/user-attachments/assets/1dd1f696-7e0e-46d4-a089-2e1f0bb4f91c" />

<img width="1247" height="932" alt="dns2" src="https://github.com/user-attachments/assets/dfe77cb1-de80-4544-a4f3-92a8ea14fba9" />

<img width="1455" height="942" alt="dns3" src="https://github.com/user-attachments/assets/bddebb2e-170b-406c-8f05-ff5bb8563c9c" />

-For the DNS changes to take affect we will restart our virtual machine Dc-1, and then log back in to our windows virtual machine (client-1) We will be sending a ping to eunsure connectivity is established between both virtual machines.

-Once logged in to client-1 windows machine open up powershell and run the command Ping along with dc-1 private i.p adress (ping 10.0.0.4)

 <img width="1283" height="706" alt="replyyy" src="https://github.com/user-attachments/assets/ab681b5e-7b6b-460c-98ad-065f03ff1ca3" />

-We can see we got a reply from dc-1 confirming a succesfull connection between both virtual machines.

<h2>Step 2: Deploy and install Active Directory</h2>

-within the server manager dashboard in our domain contollers virtual machine (dc-1) we navigate to the add roles and features tab. 

<img width="1375" height="1023" alt="Capture4" src="https://github.com/user-attachments/assets/f6b5c0b8-3c85-49d5-8503-1fe5ddd2c68e" />

<img width="1341" height="761" alt="Capture5" src="https://github.com/user-attachments/assets/b7a157c9-38f2-408e-b288-791979bc8923" />

<img width="1074" height="745" alt="Capture6" src="https://github.com/user-attachments/assets/6498ff13-8592-416e-a8b3-355eed4cc315" />

<img width="1336" height="800" alt="Capture7" src="https://github.com/user-attachments/assets/e997eae4-391c-4924-9016-6af19ae14984" />

 <img width="1318" height="820" alt="Capture8" src="https://github.com/user-attachments/assets/c7c7f8b5-33ae-4a90-ae8e-18457ca999a9" />

-After successfully installing active directory we will be promoting dc-1 as our actual domain controller.

<img width="1891" height="955" alt="Capture10" src="https://github.com/user-attachments/assets/98afb894-9e7e-4125-b86e-2c682015a7c5" />

  <img width="1219" height="808" alt="Capture9" src="https://github.com/user-attachments/assets/787f8f4f-ac21-4510-8dcd-c57aef940ab6" />

<img width="1107" height="828" alt="Capture11" src="https://github.com/user-attachments/assets/328964e1-4ed6-43d8-ba65-660c22662479" />

-Once the VM has restarted we log back in using the credentials we created along with mydomain.com\labuser

<img width="981" height="887" alt="nnnnjnjnjnn" src="https://github.com/user-attachments/assets/996c2818-1b05-461e-b0e2-78a426806969" />

<h2>Step 3: </h2>



<h2>Step 4: Create Administrative User and Organizational Units in Active Directory</h2>
<ul>
- Open Active Directory Users and Computers (ADUC) on DC-1.

- Create the following Organizational Units (OUs) to structure directory objects:

- _EMPLOYEES – for general employee user accounts

- _ADMINS – for administrative accounts

- _CLIENTS – for client-specific resources or users
<img width="531" height="367" alt="Capture7" src="https://github.com/user-attachments/assets/05f4cb7f-aec0-4866-8f69-8625231a8f6a" />

- Within the _ADMINS OU, create a new user account:

- Full Name: Jane Doe

- Username: jane_admin

- Add jane_admin to the Domain Admins security group to grant administrative privileges.
<img width="591" height="534" alt="Capture8" src="https://github.com/user-attachments/assets/c4d2cc8c-ee1d-4578-a28c-d0bf09656e9f" />

- Log out of DC-1 and sign back in using the new domain admin account:

- mydomain.com\jane_admin

<h2>Step 5: Join Client-1 to the Domain</h2>
<ul>
- In the Azure Portal, update Client-1's DNS server settings to point to DC-1's private IP address.

- Restart Client-1 from the portal to apply the new DNS configuration.

- Log in to Client-1 using the local administrator account (labuser), and join the machine to the domain mydomain.com.

- After a successful domain join, restart the VM and verify that Client-1 now appears in Active Directory Users and Computers (ADUC) under the Computers container.

- (Optional) For better organization, create an OU named _CLIENTS and move Client-1 into it.

<h2>Step 6: Enable Remote Desktop Access for Domain Users via Group Policy</h2>
<ul><img width="780" height="497" alt="Screenshot 2025-10-23 135330" src="https://github.com/user-attachments/assets/3f2c30d2-1e12-4111-b176-3b1b2acd0613" />

- Create and apply a Group Policy Object (GPO) targeting the _CLIENTS and _EMPLOYEES Organizational Units to allow domain users to connect via Remote Desktop.

- This approach ensures centralized management of Remote Desktop settings, eliminating the need for manual configuration on each individual client machine.

- To confirm the policy is applied, run the following command on affected client machines:

<h2>Step 7: Automate User Account Creation with PowerShell and Verify Access</h2>
<ul>
- Log in to DC-1 as jane_admin, and launch PowerShell ISE with administrative privileges.

- Write or run a PowerShell script to automate the creation of multiple Active Directory user accounts, specifying the appropriate OU placement for each user.
<img width="1836" height="978" alt="Capture3" src="https://github.com/user-attachments/assets/46714a87-3e2c-4dcd-8d25-02ac7a8b1976" />


- After the script executes, open Active Directory Users and Computers (ADUC) to verify that all users have been successfully created in the intended Organizational Unit.
<img width="1032" height="711" alt="Capture4" src="https://github.com/user-attachments/assets/49c7de76-fc05-40e8-a75b-c38958c128a2" />

Test account functionality by logging into Client-1 with one of the newly created user credentials to confirm successful domain authentication and Remote Desktop access (if applicable).
<h2>Conclusion</h2>

This lab demonstrated the end-to-end deployment and configuration of a functional Active Directory environment in Microsoft Azure. We provisioned a Domain Controller and a client virtual machine, configured network settings to enable communication, and installed Active Directory Domain Services (AD DS).

We established a new domain, structured the directory using Organizational Units (OUs), and created both administrative and standard user accounts. The client machine was successfully joined to the domain, and Remote Desktop access was enabled for domain users via Group Policy.

To streamline user management, we utilized PowerShell scripting to automate the creation of multiple AD user accounts and verified access by logging into the client with one of the new accounts.

This hands-on lab provided practical experience in deploying, managing, and securing an Active Directory environment—core skills for any systems administrator or cloud engineer.
