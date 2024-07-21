<br />
</p>
<p align="center">
<img src="https://static.wixstatic.com/shapes/2ebf04_1a0a78f30bf34163afef25e7e8f6f848.svg" alt="Microsoft Active Directory Logo"/>
</p>
<br />

<h1>On-Premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial provides a comprehensive guide to the implementation of on-premises Active Directory (AD) on Azure Virtual Machines (VMs). It covers the technical aspects involved in setting up and configuring AD within an Azure VM environment, including the necessary network infrastructure, domain controller deployment, and synchronization of AD with on-premises directory services.<br />




</p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Active Directory Domain Services
- PowerShell ISE

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create an Azure virtual network: To set up Active Directory, you'll first need to create an Azure virtual network to which your virtual machines will be connected. You can create this virtual network using the Azure Portal.
- Create a virtual machine: You'll need to create a virtual machine that will act as the Active Directory domain controller. You can use one of the pre-built images available in the Azure, or you can create a custom virtual machine image.
- Install Active Directory Domain Services: Once you have created the virtual machine, you will need to install Active Directory Domain Services on it. This involves adding the Active Directory Domain Services role to the server and running the necessary configuration wizards.
- Configure DNS: As part of the Active Directory setup process, you will need to configure DNS. This involves setting up a DNS server on the domain controller virtual machine and configuring your virtual network to use this DNS server.
- Join other virtual machines to the domain: Once you have set up the domain controller virtual machine and configured DNS, you can join other virtual machines to the domain. This involves changing the network settings on the virtual machines to use the DNS server you set up in step 4 and joining the virtual machines to the domain using the Active Directory Domain Services configuration.
- Configure Active Directory Group Policies: After joining the virtual machines to the domain, you can use Active Directory Group Policies to manage and configure the virtual machines.

<h2>Deployment and Configuration Steps</h2>

<p>
<p align="center"> 
<img width="1118" alt="Step 1" src="https://github.com/user-attachments/assets/766e6fd4-173e-4b10-acca-5df6947ea760">
</p>
<p>
Step 1: Create a resource group that can be utilized on both virtual machines (VM).
</p>
<br />

<p>
<p align="center"> 
<img width="823" alt="Step 2" src="https://github.com/user-attachments/assets/b1c6a022-36b0-41b5-8bfd-7b11298165ac">
</p>
<p>
Step 2: Set up the domain controller running Active Directory by creating the first virtual machine with Windows Server 2022 as the image.
</p>
<br />

<p>
<p align="center"> 
<img width="674" alt="Step 3" src="https://github.com/user-attachments/assets/b320373d-5b82-41f9-9791-0cee12998aff">
</p>
<p>
Step 3: Create a username and password for the Windows Server virtual machine, then click on "Review + Create".
</p>
<br />

<p>
<p align="center"> 
<img width="841" alt="Step 4" src="https://github.com/user-attachments/assets/6f194a5a-c245-46a9-9e8f-1f70b4ddadae">
</p>
<p>
Step 4: Set up the second virtual machine with Windows 10 Pro, Version 21H2, create a username and password, then click on "Review + Create".
</p>
<br />

<p>
<p align="center"> 
<img width="830" alt="Step 5" src="https://github.com/user-attachments/assets/221e932d-1130-429e-ae9d-f0c5f92c01f0">
</p>
<p>
Step 5: Ensure that VM2 running Windows 10 Pro is added to the same virtual network and resource group as VM1 running Windows Server, by going to the networking tab.
</p>
<br />

<p>
<p align="center"> 
<img width="1100" alt="Step 6" src="https://github.com/user-attachments/assets/c2d31dbf-f4ec-4bac-b32e-c8267b9e7d62">
</p>
<p>
Step 6: Navigate to the Azure virtual machines and select Virtual Machine 1, then click on "Networkin Settings" and choose "Network interface".
</p>
<br />

<p>
<p align="center"> 
<img width="1119" alt="Step 7" src="https://github.com/user-attachments/assets/25caa60b-c031-4872-a770-c526acde47b1">
</p>
<p>
Step 7: Proceed to "IP Configurations" and select "ipconfig 1".
</p>
<br />

<p>
<p align="center"> 
<img width="1119" alt="Step 7" src="https://github.com/user-attachments/assets/69a6e4fc-b665-48ed-94a7-f0ce1d000829">
</p>
<p>
Step 8: Switch the Private IP address assignment from Dynamic to Static, then select "Save".
</p>
<br />

<p>
<p align="center"> 
<img width="1108" alt="image" src="https://github.com/user-attachments/assets/59f6a995-513c-4287-8004-2ca7ca5256b9">
</p>
<p>
Step 9: Use Remote Desktop Connection to connect to VM1 using its public IP address.
</p>
<br />

<p>
<p align="center"> 
<img width="1106" alt="Step 8" src="https://github.com/user-attachments/assets/d9855eea-9b43-4dcf-9f17-6a975c73c9c7">
</p>
<p>
Step 10: Once logged into the virtual machine, navigate to Windows Defender Firewall with Advanced Security, and click on Inbound Security Rules. Enable the following rules:
<ul>
<li>Core Networking Diagnostics – ICMP Echo Request (ICMPv4-In) from <b><i>any remote address</b></i>.</li>
<li>Core Networking Diagnostics – ICMP Echo Request (ICMPv4-In) from <b><i>the local subnet</b></i>.</li>
</ul> 
</p>
<br />

<p>
<p align="center"> 
<img width="1091" alt="Step 9" src="https://github.com/user-attachments/assets/e4574252-9a42-4c5a-8acf-25315e95530c">
</p>
<p>
Step 11: Open Server Manager and select "Add Roles and Features."
</p>
<br />

<p>
<p align="center"> 
<img width="585" alt="Step 10" src="https://github.com/user-attachments/assets/6a4725fa-ed10-4d90-bf27-db1299f504f1">
</p>
<p>
Step 12: Follow the default installation settings until you reach "Server Roles." Select "Active Directory Domain Services" and click "Next."
</p>
<br />

<p>
<p align="center"> 
<img width="588" alt="Step 11" src="https://github.com/user-attachments/assets/7cc8e743-6125-4048-a926-2ba512e9c1e5">
</p>
<p>
Step 13: Continue with the default installation settings until the final page, then click "Install."
</p>
<br />

<p>
<p align="center"> 
<img width="1091" alt="Step 12" src="https://github.com/user-attachments/assets/0097fa08-0149-4de8-9520-5bf67cd5af31">
</p>
<p>
Step 14: Click on the flag icon in Server Manager with the yellow warning sign and select "Promote this server to a domain controller."
</p>
<br />

<p>
<p align="center"> 
<img width="568" alt="Step 13" src="https://github.com/user-attachments/assets/de7fc1d6-83d2-4504-8f37-aaaed2b87f9b">
</p>
<p>
Step 15: Select "Add a new forest" and choose a domain name for the root.
</p>
<br />

<p>
<p align="center"> 
<img width="572" alt="Step 14" src="https://github.com/user-attachments/assets/4e656945-5fe1-4165-b092-f167b1e865c9">
</p>
<p>
Step 16: Choose a password for Directory Services Restore Mode (DSRM).
</p>
<br />

<p>
<p align="center"> 
<img width="572" alt="Step 15" src="https://github.com/user-attachments/assets/fee871a6-c8ed-4c77-8376-415c0e511d1c">
</p>
<p>
Step 17: Proceed with the default installation settings and click the "Install" button.
</p>
<br />

<p>
<p align="center"> 
<img width="505" alt="Step 16" src="https://github.com/user-attachments/assets/79d92ac9-663c-4139-ba8b-3aaaf036504d">
</p>
<p>
Step 18: After successfully installing Active Directory Domain Services, the remote desktop connection will automatically restart.
</p>
<br />

<p>
<p align="center"> 
<img width="337" alt="Step 17" src="https://github.com/user-attachments/assets/40d7bc5c-589b-435e-bb3d-7adaf33f1695">
</p>
<p>
Step 19: To log back into the virtual machine, use Remote Desktop Connection with the domain name chosen for root followed by a backslash and the username you selected for the VM. Enter the password and click on the "Ok" button.
</p>
<br />

<p>
<p align="center"> 
<img width="1085" alt="Step 18" src="https://github.com/user-attachments/assets/476488c4-88a7-49cf-9d29-c813fda1af9a">
</p>
<p>
Step 20: To organize users into different categories, navigate to Tools in Server Manager and select Active Directory Users and Computers.
</p>
<br />

<p>
<p align="center"> 
<img width="323" alt="Step 19" src="https://github.com/user-attachments/assets/52f52361-3a96-4587-93a2-0d4ebe3208f1">
</p>
<p>
Step 21: Create two folders named "Employees" and "Admins" by right-clicking on the created domain, select "New", then choose "Organizational Unit" in Server Manager.
</p>
<br />

<p>
<p align="center"> 
<img width="323" alt="Step 20" src="https://github.com/user-attachments/assets/96d02ab7-bd55-4a99-b215-1e8590c0a595">
</p>
<p>
Step 22: Navigate to the newly created "Admins" folder, then select "New" and choose "User" to create a user account. that with administrative privileges.
</p>
<br />

<p>
<p align="center"> 
<img width="424" alt="Step 21" src="https://github.com/user-attachments/assets/34f09d05-5e97-4d9b-b7be-f94924fa9723">
</p>
<p>
Step 23: To give the newly created user administrative privileges, right-click on the user in the Admins folder and select Properties. Then, navigate to the "Member of" tab and click on "Add". Finally, add the user to the Domain Admins group.
</p>
<br />

<p>
<p align="center"> 
<img width="332" alt="Step 22" src="https://github.com/user-attachments/assets/e63a5825-bdbe-4fca-9892-614a093ee978">
</p>
<p>
Step 24: After logging off, use the remote desktop connection to access the domain controller with the newly created admin user.
</p>
<br />

<p>
<p align="center"> 
<img width="1112" alt="Step 23" src="https://github.com/user-attachments/assets/7bb971de-ab72-49c9-b229-2b0dc58ea1f2">

</p>
<p>
Step 25: Return to the Azure portal on your local computer and navigate to Virtual Machine 1. Then, go to Networking and copy the NIC Private IP. Finally, update virtual machine 2's DNS to match this IP address.
</p>
<br />

<p>
<p align="center"> 
<img width="1091" alt="Step 24" src="https://github.com/user-attachments/assets/17a526ac-12bd-48d9-8670-0f69d28e9cc7">
</p>
<p>
Step 26: Navigate to the Network Interface section of virtual machine 2 in the Azure Portal.
</p>
<br />

<p>
<p align="center"> 
<img width="727" alt="Step 25" src="https://github.com/user-attachments/assets/e661e344-14fe-4852-bc4a-f6782b1046d9">
</p>
<p>
Step 27: Navigate to Network Interface in the Azure Portal for virtual machine 2. Then, select DNS Servers and choose "Custom" to update the DNS Server settings with virtual machine 1's Private IP. Finally, click on "Save" to save the changes.
</p>
<br />

<p>
<p align="center"> 
<img width="715" alt="Step 26" src="https://github.com/user-attachments/assets/7aae2a4e-443b-4635-8c19-6f7fe5856dbc">
</p>
<p>
Step 28: Use the selected username and password during the initial setup of the Windows 10 virtual machine to re-establish a Remote Desktop Connection.
</p>
<br />

<p>
<p align="center"> 
<img width="302" alt="Step 27" src="https://github.com/user-attachments/assets/41ba600f-22cc-4b59-9a5b-9d37714d7428">
</p>
<p>
Step 29: Right-click the Windows logo located in the bottom left corner of the screen, select "System", then "About", and click on "Rename this PC (advanced)" followed by "Change".
</p>
<br />

<p>
<p align="center"> 
<img width="713" alt="Step 28" src="https://github.com/user-attachments/assets/b27deec7-b2ce-4557-9b47-c4e6fb6837a8">
</p>
<p>
Step 30: Next, click on "Domain" under the "Member of" section and enter the domain name that was previously chosen for root, click "OK", and provide the username and password of the admin user.
</p>
<br />

<p>
<p align="center"> 
<img width="234" alt="Step 29" src="https://github.com/user-attachments/assets/8a309a9d-5abf-45ee-8185-3b75466e94fe">
</p>
<p>
Step 31: In the event that the joining of VM2 to the domain controller VM1 is successful, a welcome message should be received.
</p>
<br />

<p>
<p align="center"> 
<img width="260" alt="Step 30" src="https://github.com/user-attachments/assets/df6585f5-035a-4944-bab6-b00fd238f3b3">
</p>
<p>
Step 32: After successfully joining the domain controller, a machine restart will be initiated to apply the changes.
</p>
<br />

<p>
<p align="center"> 
<img width="893" alt="Step 31" src="https://github.com/user-attachments/assets/41f4c821-c53d-488b-82df-456ca9df26af">
</p>
<p>
Step 33: To proceed, remotely connect back to VM2 using the admin user credentials, then navigate to "System", go to "About", followed by "Remote Desktop", and click on “select users that can remotely access this pc".
</p>
<br />

<p>
<p align="center"> 
<img width="340" alt="Step 32" src="https://github.com/user-attachments/assets/49951f6a-f521-4b20-bfe2-dd8b2509fd03">
</p>
<p align="center"> 
<img width="280" alt="Step 32 -2" src="https://github.com/user-attachments/assets/0fde4566-2a29-40db-bba4-b3f2a4aa8546">
</p>
<p>
Step 34: Subsequently, click on "Add", enter "Domain Users", and click "OK" to grant access to <b><i>all</b></i> user accounts created in Active Directory to the domain controller.
</p>
<br />

<p>
<p align="center"> 
<img width="588" alt="Step 33" src="https://github.com/user-attachments/assets/26480329-ebe6-4000-9ce0-071bf91f3a92">
</p>
<p>
Step 35: Launch Windows PowerShell ISE with administrator privileges to create additional user accounts.
</p>
<br />

<p>
<p align="center"> 
<img width="1004" alt="Step 34" src="https://github.com/user-attachments/assets/dec52833-ea23-4f9c-8bbb-b85cb61a82d2">
</p>
<p>
Step 36: Copy and paste the code provided in the <a href=https://github.com/MalikS-Github/configure-ad/blob/main/Code%20to%20Create%20Users>text document</a> uploaded to this tutorial into PowerShell ISE.
</p>
<br />

<p>
<p align="center"> 
<img width="1106" alt="Step 35" src="https://github.com/user-attachments/assets/1f65984a-fccd-414f-aad1-0c28ed14f032">

</p>
<p>
Step 37: Open PowerShell ISE, create a new script, paste the provided code, and click the green "run script" button.
</p>
<br />

<p>
<p align="center"> 
<img width="559" alt="Step 36" src="https://github.com/user-attachments/assets/2f7cbcd3-5496-4114-b29c-479d8f198397">
</p>
<p>
Step 38 – If the aforementioned steps were executed correctly, user accounts should start to generate within PowerShell.
</p>
<br />

<p>
<p align="center"> 
<img width="1094" alt="Step 37" src="https://github.com/user-attachments/assets/ef32de55-f915-4cce-bde0-d5238eec4bea">
</p>
<p>
Step 39: Launch Active Directory Users and Computers in Server Manager and observe the various accounts populating in the Employees folder.
</p>
<br />

<p>
<p align="center"> 
<img width="709" alt="Step 38" src="https://github.com/user-attachments/assets/2a7c1f9f-80be-41a5-a023-94c480b12828">
</p>
<p>
Step 40: Select a user account at random and try to log into virtual machine 2 using the default password assigned to all user accounts, which is "Password1".
</p>
<br />

<p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_d78f58f24a0849af83920875e19bbb91~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p align="center"> 
<img src="https://static.wixstatic.com/media/2ebf04_61d6255d81ee411e93fde25cd355a124~mv2.png" height="60%" width="60%" alt="Configuring On-premises Active Directory within Azure VMs"/>
</p>
<p>
Step 41: Once a user account on Active Directory is successfully logged in, this lab will conclude. In addition, several other account options are available, including the capability to unlock "locked" user accounts due to failed password attempts, reset passwords, disable accounts, and more.
</p>
<br />

