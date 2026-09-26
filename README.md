# active-directory-<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>

This repository demonstrates the implementation of an on-premises-style Active Directory infrastructure within Azure Virtual Machines (VMs). The steps outline the process of creating a Domain Controller (DC) and a client machine, establishing connectivity, and configuring the necessary network and DNS settings for Active Directory Domain Services

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

**1. Install Active Directory**
- Login to `DC-1`
  - Use the credentials:
    - Username: 
    - Password: 
- Install Active Directory Domain Services
  - Open Server Manager and install the Active Directory Domain Services role.
- Promote as a Domain Controller
  - Set up a new forest with the domain name `mydomain.com` (or any preferred name).
  - Restart the server after promotion.
- Login to `DC-1` as Domain User
  - Use the credentials:
    - Username: `mydomain.com\`

<img width="50%" height="50%" alt="Screenshot 2026-07-13 112549" src="https://github.com/user-attachments/assets/7e95a0fa-ca14-4f35-bed5-919977a8ddf8" />

<img width="50%" height="50%" alt="Screenshot 2026-07-13 112947" src="https://github.com/user-attachments/assets/0ec387dc-42d8-4706-b578-d2ca178eefce" />

<img width="50%" height="50%" alt="Screenshot 2026-07-13 113042" src="https://github.com/user-attachments/assets/9ffbb54e-d477-4ae2-8691-aa65d5fb6a34" />

 <li><strong> Since its our first time logging in we will get this security prompt click yes and we will be connected to our domain controllers virtual machine (dc-1)
 
<img width="50%" height="50%" alt="Capture" src="https://github.com/user-attachments/assets/a551088b-220e-4eec-8712-ed306b0ea8c4" />

<li><strong> We succesfully connected to our virtual machine now we will disable our windows firewall using the comman "wf.msc" we are disabling to be able to send out a virtual continous ping to ensure both our virtual machines are able to connect to eachother.

<img width="50%" height="50%" alt="Capture2" src="https://github.com/user-attachments/assets/b517c55b-0104-4abc-8224-03484c7a5bf8" />

<img width="50%" height="50%" alt="Capture3" src="https://github.com/user-attachments/assets/51e773c4-a7ba-4161-8bcb-5c5c65e04479" />

<li><strong> The next step is too set Client-1’s DNS settings to DC-1’s Private IP address within our azure portal we go to client-1 NIC and paste dc-1 private address

<img width="50%" height="50%" alt="dns" src="https://github.com/user-attachments/assets/1dd1f696-7e0e-46d4-a089-2e1f0bb4f91c" />

<img width="50%" height="50%" alt="dns2" src="https://github.com/user-attachments/assets/dfe77cb1-de80-4544-a4f3-92a8ea14fba9" />

<img width="50%" height="50%" alt="50%" src="https://github.com/user-attachments/assets/bddebb2e-170b-406c-8f05-ff5bb8563c9c" />

<li><strong> For the DNS changes to take affect we will restart our virtual machine Dc-1, and then log back in to our windows virtual machine (client-1) We will be sending a ping to eunsure connectivity is established between both virtual machines.

<li><strong> Once logged in to client-1 windows machine open up powershell and run the command Ping along with dc-1 private i.p adress (ping 10.0.0.4)

 <img width="50%" height="50%" alt="replyyy" src="https://github.com/user-attachments/assets/ab681b5e-7b6b-460c-98ad-065f03ff1ca3" />

<li><strong> We can see we got a reply from dc-1 confirming a succesfull connection between both virtual machines.

<h2>Step 2: Deploy and install Active Directory</h2>

<li><strong> Within the server manager dashboard in our domain contollers virtual machine (dc-1) we navigate to the add roles and features tab. 

<img width="50%" height="50%" alt="Capture4" src="https://github.com/user-attachments/assets/f6b5c0b8-3c85-49d5-8503-1fe5ddd2c68e" />

<img width="50%" height="50%" alt="Capture5" src="https://github.com/user-attachments/assets/b7a157c9-38f2-408e-b288-791979bc8923" />

<img width="50%" height="50%" alt="Capture6" src="https://github.com/user-attachments/assets/6498ff13-8592-416e-a8b3-355eed4cc315" />

<img width="50%" height="50%" alt="Capture7" src="https://github.com/user-attachments/assets/e997eae4-391c-4924-9016-6af19ae14984" />

 <img width="50%" height="50%" alt="Capture8" src="https://github.com/user-attachments/assets/c7c7f8b5-33ae-4a90-ae8e-18457ca999a9" />

<li><strong> After successfully installing active directory we will be promoting dc-1 as our actual domain controller.

<img width="50%" height="50%" alt="Capture10" src="https://github.com/user-attachments/assets/98afb894-9e7e-4125-b86e-2c682015a7c5" />

  <img width="50%" height="50%" alt="Capture9" src="https://github.com/user-attachments/assets/787f8f4f-ac21-4510-8dcd-c57aef940ab6" />

<img width="50%" height="50%" alt="Capture11" src="https://github.com/user-attachments/assets/328964e1-4ed6-43d8-ba65-660c22662479" />

<li><strong> Once the VM has restarted we log back in using the credentials we created along with mydomain.com\labuser

<img width="50%" height="50%" alt="nnnnjnjnjnn" src="https://github.com/user-attachments/assets/996c2818-1b05-461e-b0e2-78a426806969" />

**2. Create a Domain Admin User**
- Open Active Directory Users and Computers (ADUC)
- Create Organizational Units (OUs)
  - Create an OU named `_EMPLOYEES`.
  - Create another OU named `_ADMINS`.
- Create a New Employee User
  - Add a user named "Jane Doe" with the following details:
    - Username: `jane_admin`
    - Password: `Cyberlab123!`
- Add User to Security Group
  - Add `jane_admin` to the Domain Admins Security Group.
- Log in as `jane_admin`
  - Log out from `DC-1` and log back in using:
    - Username: `mydomain.com\jane_admin`
    - Password: `Cyberlab123!`
  - Use `jane_admin` as the admin account from this point forward.12" src="https://github.com/user-attachments/assets/f753062c-f90c-4d0b-8345-c41422fd2c5b" />

- Create the following Organizational Units (OUs) to structure directory objects:

- _EMPLOYEES – for general employee user accounts

<img width="50%" height="50%" alt="Capture14" src="https://github.com/user-attachments/assets/8253aa91-adf9-4c0a-8deb-af32294893e3" />

- _ADMINS – for administrative accounts
- 
<img width="50%" height="50%" alt="Capture7" src="https://github.com/user-attachments/assets/05f4cb7f-aec0-4866-8f69-8625231a8f6a" />

- Within the _ADMINS OU, create a new user account:

- Full Name: Jane Doe

- Username: jane_admin

<img width="50%" height="50%" alt="Capture8" src="https://github.com/user-attachments/assets/c4d2cc8c-ee1d-4578-a28c-d0bf09656e9f" />

<img width="50%" height="50%" alt="Capturr21" src="https://github.com/user-attachments/assets/0bfaa8c2-2cc6-48dc-b85c-ef6ed01989bf" />

- Add jane_admin to the Domain Admins security group to grant administrative privileges.

<img width="50%" height="50%" alt="Capture22" src="https://github.com/user-attachments/assets/c45a698a-166b-4f2c-9053-97a14a7f6d94" />


Join `Client-1` to the Domain**
- Login to `Client-1` as Local Admin
- Join `Client-1` to the Domain
  - Change the system properties to join the domain `mydomain.com.`
  - Restart `Client-1` after joining.
- Verify in ADUC
  - Log in to `DC-1` and confirm that `Client-1` appears in the Active Directory Users and Computers tool.
- Organize `Client-1` in ADUC
  - Create an OU named `_CLIENTS`.
  - Drag `Client-1` into the `_CLIENTS OU`.


- Log out of DC-1 and sign back in using the new domain admin account: mydomain.com\jane_admin

- Log in to Client-1 as the original local admin (labuser) and join it to the domain.

<img width="50%" height="50%" alt="tttttttttttttt" src="https://github.com/user-attachments/assets/4ec13030-de1b-4b94-a957-f1f54240bccf" />

<img width="50%" height="50%" alt="mydomain" src="https://github.com/user-attachments/assets/135cb99b-6d41-4a9f-b68b-4079782ecac1" />

<img width="50%" height="50%" alt="dmnnn" src="https://github.com/user-attachments/assets/562381ed-df4c-4db4-8b1f-e1d046f1c591" />


- After a successful domain join, restart the VM and verify that Client-1 now appears in Active Directory Users and Computers under the Computers container in our dc-1 VM (domain controller)

<img width="50%" height="50%" alt="bbbbbbbbbbbbbb" src="https://github.com/user-attachments/assets/ce35f5c6-facc-49e6-b6c1-a1f37b7ace45" />

 For better organization, create an OU named _CLIENTS and move Client-1 into it.

<img width="50%" height="50%" alt="CCCCCCCCCCC" src="https://github.com/user-attachments/assets/f3fe7c76-a12e-4dcd-aceb-fec440fd94c1" />

<img width="50%" height="50%" alt="DDDDDDDDDDD" src="https://github.com/user-attachments/assets/ecc0477b-5244-4d5d-99a1-71dc7ed19302" />



**4. Setup Remote Desktop for Non-Administrative Users on Client-1**

- Login to `Client-1` as `mydomain.com\jane_admin`
  - Use the credentials for `jane_admin`.
- Allow Domain Users Access to Remote Desktop
  - Open system properties.
  - Click on "Remote Desktop."
  - Allow "domain users" access to Remote Desktop.
- Test Remote Desktop Access
  - You can now log into `Client-1` as a normal, non-administrative user.
   -Note: Typically, this configuration is managed using Group Policy for multiple systems.




-Go to system settings and click on the remote desktop tab in dc-1 as you can see we are logged in as administrator jane doe.

<img width="50%" height="50%" alt="remote desktop" src="https://github.com/user-attachments/assets/6ad01e46-72e9-4487-b24b-960f3a75f16d" />


<img width="50%" height="50%" alt="jane doe" src="https://github.com/user-attachments/assets/c6847ab5-ee83-4b6a-913e-1a39c68e46cd" />

>
<img width="50%" height="50%" alt="rererereer" src="https://github.com/user-attachments/assets/08faee75-7ce5-476b-ab6b-792f34cafe85" />


<img width="50%" height="50%" alt="rorororor" src="https://github.com/user-attachments/assets/b2b8518f-3101-41e0-85e6-58d38aa0b8c3" />

-we are allowing all the domain users to be able to use remote desktop this


Step 6
- Login to `DC-1` as `jane_admin`
  - Use the credentials for `jane_admin`.
- Open PowerShell ISE as Administrator
  - Launch PowerShell ISE with administrative privileges.
- Create Users with a Script
  - Create a new file and paste the provided [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into it.
  - Run the script to create multiple user accounts.
- Verify Accounts in ADUC
  - Open Active Directory Users and Computers (ADUC).
  - Observe the newly created accounts in the `_EMPLOYEES OU`.
- Test Login
  - Attempt to log into `Client-1` using one of the newly created accounts.
  - Ensure the account password matches what is specified in the script.


- Log in to DC-1 as jane_admin, and launch PowerShell ISE with administrative privileges.

- Write or run a PowerShell script to automate the creation of multiple Active Directory user accounts, specifying the appropriate OU placement for each user.
<img width="50%" height="50%" alt="Capture3" src="https://github.com/user-attachments/assets/46714a87-3e2c-4dcd-8d25-02ac7a8b1976" />


- After the script executes, open Active Directory Users and Computers (ADUC) to verify that all users have been successfully created in the intended Organizational Unit.
<img width="50%" height="50%" alt="Capture4" src="https://github.com/user-attachments/assets/49c7de76-fc05-40e8-a75b-c38958c128a2" />

Test account functionality by logging into Client-1 with one of the newly created user credentials to confirm successful domain authentication and Remote Desktop access (if applicable).
<h2>Conclusion</h2>

This lab demonstrated the end-to-end deployment and configuration of a functional Active Directory environment in Microsoft Azure. We provisioned a Domain Controller and a client virtual machine, configured network settings to enable communication, and installed Active Directory Domain Services (AD DS).

We established a new domain, structured the directory using Organizational Units (OUs), and created both administrative and standard user accounts. The client machine was successfully joined to the domain, and Remote Desktop access was enabled for domain users via Group Policy.

To streamline user management, we utilized PowerShell scripting to automate the creation of multiple AD user accounts and verified access by logging into the client with one of the new accounts.

This hands-on lab provided practical experience in deploying, managing, and securing an Active Directory environment—core skills for any systems administrator or cloud engineer.
