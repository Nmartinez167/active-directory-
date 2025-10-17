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

- Deploy a Windows Server 2022 virtual machine to serve as the Domain Controller, and name it DC-1.

- Note the Resource Group and Virtual Network (VNet) associated with the Domain Controller for later configuration.

- Configure the network interface (NIC) of DC-1 to use a static private IP address to ensure reliable connectivity.<img width="1871" height="796" alt="Screenshot 2025-10-16 082844" src="https://github.com/user-attachments/assets/b6aa37c2-5f8c-4aaa-8039-af05b0275cce" />


- Create a Windows 10 virtual machine named Client-1 within the same Resource Group and VNet as DC-1.

- Verify that both DC-1 and Client-1 reside within the same virtual network by using Azure Network Watcher's topology tool.

<h2>Step 2: Verify Connectivity Between Client and Domain Controller</h2>
<ul>
<img width="1712" height="882" alt="Screenshot 2025-10-17 132701" src="https://github.com/user-attachments/assets/2b3ee7e0-9e7e-45b6-9334-644137542a59" />

- Connect to Client-1 via Remote Desktop, and initiate a continuous ping to DC-1's private IP address

  
<h2>Step 3: Install and Configure Active Directory</h2>
<ul>
- Log in to DC-1 and install the Active Directory Domain Services (AD DS) role via Server Manager.

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

- Within the _ADMINS OU, create a new user account:

- Full Name: Jane Doe

- Username: jane_admin

- Add jane_admin to the Domain Admins security group to grant administrative privileges.

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
<ul>
- Create and apply a Group Policy Object (GPO) targeting the _CLIENTS and _EMPLOYEES Organizational Units to allow domain users to connect via Remote Desktop.

- This approach ensures centralized management of Remote Desktop settings, eliminating the need for manual configuration on each individual client machine.

- To confirm the policy is applied, run the following command on affected client machines:

<h2>Step 7: Automate User Account Creation with PowerShell and Verify Access</h2>
<ul>
- Log in to DC-1 as jane_admin, and launch PowerShell ISE with administrative privileges.

- Write or run a PowerShell script to automate the creation of multiple Active Directory user accounts, specifying the appropriate OU placement for each user.

- After the script executes, open Active Directory Users and Computers (ADUC) to verify that all users have been successfully created in the intended Organizational Unit.

Test account functionality by logging into Client-1 with one of the newly created user credentials to confirm successful domain authentication and Remote Desktop access (if applicable).
<h2>Conclusion</h2>

This lab demonstrated the end-to-end deployment and configuration of a functional Active Directory environment in Microsoft Azure. We provisioned a Domain Controller and a client virtual machine, configured network settings to enable communication, and installed Active Directory Domain Services (AD DS).

We established a new domain, structured the directory using Organizational Units (OUs), and created both administrative and standard user accounts. The client machine was successfully joined to the domain, and Remote Desktop access was enabled for domain users via Group Policy.

To streamline user management, we utilized PowerShell scripting to automate the creation of multiple AD user accounts and verified access by logging into the client with one of the new accounts.

This hands-on lab provided practical experience in deploying, managing, and securing an Active Directory environment—core skills for any systems administrator or cloud engineer.
