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

- next we will be logging into our virtual machine (dc-1) our virtual machine we will be using as a domain controller to shut off the windows firewall to ensure connection between both of our virtual machines, this is not recommendedthis is just for demonstration purposes.


- After our virtual machines are created, set Client-1’s DNS settings to DC-1’s Private IP address this will alow a connection between both virtual machines.


<h2>Step 2: Verify Connectivity Between Client and Domain Controller</h2>
<ul>
<img width="1712" height="882" alt="Screenshot 2025-10-17 132701" src="https://github.com/user-attachments/assets/2b3ee7e0-9e7e-45b6-9334-644137542a59" />

- Connect to Client-1 via Remote Desktop, and initiate a continuous ping to DC-1's private IP address

  
<h2>Step 3: Install and Configure Active Directory</h2>
<ul>
- Log in to DC-1 and install the Active Directory Domain Services (AD DS) role via Server Manager.
<img width="1055" height="766" alt="Capture5" src="https://github.com/user-attachments/assets/b0e033dd-c8e3-4e70-bdd8-60ea09cdb69d" />

- Promote DC-1 to a Domain Controller by creating a new forest, specifying a domain name (e.g., mydomain.com).

- After the promotion process completes, restart the VM and log in using your new domain credentials:

- mydomain.com\labuser

- ping -t <ip_address>

- On DC-1, enable ICMPv4 (ping) traffic through the Windows Firewall to allow incoming echo requests.
<img width="1371" height="950" alt="Capture" src="https://github.com/user-attachments/assets/45d85da3-2adf-4cbb-abc1-3be42c911cdd" />

- Return to Client-1 and confirm that the ping is now successful, verifying network connectivity between the client and domain controller.


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
