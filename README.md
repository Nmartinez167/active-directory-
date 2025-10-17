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

<li><strong>Provision Azure Resources:</strong>
Set up a Domain Controller virtual machine and a Client virtual machine within the same Azure virtual network to ensure proper communication.

<li><strong>Verify Network Connectivity:</strong>
Confirm network communication between the Client and the Domain Controller to enable domain-related operations.

<li><strong>Install Active Directory Domain Services:</strong>
Deploy the AD DS role on the Domain Controller to create and manage the Active Directory domain.

<li><strong>Create User Accounts:</strong>
Establish both administrative and standard user accounts within Active Directory to manage access and permissions.

<li><strong>Join Client to Domain:</strong>
Configure the Client machine to join the Active Directory domain for centralized authentication and resource management.

<h2>Configure Remote Desktop Access via Group Policy:</h2>
Apply Group Policy settings to allow non-administrative users in the _CLIENTS and _EMPLOYEES Organizational Units remote desktop access.

<h2>Automate User Account Creation:</h2>
Utilize PowerShell ISE scripting to bulk create user accounts and validate access to ensure proper functionality.

<h2>Deployment and Configuration Steps</h2>

Project Overview
<li><strong>This project involved the end-to-end setup of a cloud-hosted Active Directory environment using Azure Virtual Machines. I created a Windows Server 2022 Domain Controller and a Windows 10 client, ensured secure network connectivity between them, and configured essential AD components such as user accounts, Organizational Units (OUs), and Group Policy settings.

<li><strong>The lab provided hands-on experience with foundational AD tasks and demonstrated my ability to manage identity services in a cloud-based infrastructure.

<li><strong>Key Accomplishments
<li><strong>Deployed Virtual Machines:

<li><strong>Created DC-1 (Domain Controller) and Client-1 (Windows 10) within the same Azure Resource Group and Virtual Network.

<li><strong>Set the Domain Controller’s private IP address as static to ensure stable DNS resolution.

<li><strong>Established Network Connectivity:

<li><strong>Configured firewall rules and validated internal communication using ICMP (ping) between client and server VMs.

<li><strong>Installed and Configured Active Directory:

<li><strong>Installed the Active Directory Domain Services (AD DS) role on DC-1.

<li><strong>Promoted the server to a Domain Controller and set up a new forest (mydomain.com).

<li><strong>Created Organizational Units and User Accounts:

<li><strong>Created OUs: _EMPLOYEES, _ADMINS, and _CLIENTS.

<li><strong Created a domain admin account (jane_admin) and added it to the Domain Admins group.
      
<li><strongJoined Client to the Domain:

<li><strongConfigured Client-1’s DNS to point to DC-1.

<li><strongSuccessfully joined the client machine to the domain and moved it into the _CLIENTS OU.

<li><strongConfigured Remote Desktop via Group Policy:

<li><strongCreated and applied a Group Policy Object allowing Remote Desktop access for users in the _EMPLOYEES and _CLIENTS OUs.

<li><strongVerified policy application using gpupdate /force.

<li><strongAutomated User Provisioning with PowerShell:

<li><strongUsed PowerShell ISE to script the creation of multiple user accounts in Active Directory.

<li><strongVerified new user accounts and tested domain login functionality from Client-1.
Results
<li><strongSuccessfully deployed a working Active Directory environment in Azure.

<li><strongDemonstrated ability to manage domain infrastructure, user permissions, and client configuration.

<li><strongImplemented policy-based remote access and automated user management using PowerShell.

<li><strongGained practical experience in Active Directory design, deployment, and administration in a real-world, cloud-hosted environment.


