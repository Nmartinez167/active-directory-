# active-directory-<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

Project Overview
This project involved the end-to-end setup of a cloud-hosted Active Directory environment using Azure Virtual Machines. I created a Windows Server 2022 Domain Controller and a Windows 10 client, ensured secure network connectivity between them, and configured essential AD components such as user accounts, Organizational Units (OUs), and Group Policy settings.

The lab provided hands-on experience with foundational AD tasks and demonstrated my ability to manage identity services in a cloud-based infrastructure.

Key Accomplishments
Deployed Virtual Machines:

Created DC-1 (Domain Controller) and Client-1 (Windows 10) within the same Azure Resource Group and Virtual Network.

Set the Domain Controller’s private IP address as static to ensure stable DNS resolution.

Established Network Connectivity:

Configured firewall rules and validated internal communication using ICMP (ping) between client and server VMs.

Installed and Configured Active Directory:

Installed the Active Directory Domain Services (AD DS) role on DC-1.

Promoted the server to a Domain Controller and set up a new forest (mydomain.com).

Created Organizational Units and User Accounts:

Created OUs: _EMPLOYEES, _ADMINS, and _CLIENTS.

Created a domain admin account (jane_admin) and added it to the Domain Admins group.

Joined Client to the Domain:

Configured Client-1’s DNS to point to DC-1.

Successfully joined the client machine to the domain and moved it into the _CLIENTS OU.

Configured Remote Desktop via Group Policy:

Created and applied a Group Policy Object allowing Remote Desktop access for users in the _EMPLOYEES and _CLIENTS OUs.

Verified policy application using gpupdate /force.

Automated User Provisioning with PowerShell:

Used PowerShell ISE to script the creation of multiple user accounts in Active Directory.

Verified new user accounts and tested domain login functionality from Client-1.

Results
Successfully deployed a working Active Directory environment in Azure.

Demonstrated ability to manage domain infrastructure, user permissions, and client configuration.

Implemented policy-based remote access and automated user management using PowerShell.

Gained practical experience in Active Directory design, deployment, and administration in a real-world, cloud-hosted environment.


