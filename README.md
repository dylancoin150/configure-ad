<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the deployment and configuration steps of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller VMs
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join a client to your domain
- Setup Remote Desktop for non-administrative users

<h2>Deployment and Configuration Steps</h2>

1. Start by making a new virtual machine (VM) in Azure for the Domain Controller. Choose Windows Server 2022 and name the VM "DC01".

2. Once you've made the Domain Controller VM (DC01), make sure its Network Interface Card (NIC) uses a fixed private IP address. This keeps the network connection steady and helps with communication in Azure.

3. Make a new virtual machine (VM) for the client, naming it "Client01" and selecting Windows 10 as the operating system. Use the same Resource Group and Virtual Network (Vnet) that you used for the Domain Controller VM (DC01) so both machines can communicate effectively within the same network.

4. To establish connectivity between the client and Domain Controller VMs, first, log in to "Client01" using Remote Desktop. Then, initiate a continuous ping to the private IP address of "DC-1" by running the command: ping -t <ip address>, inside Command Prompt. This perpetual ping helps verify consistent communication between the client and the Domain Controller.

5. Access the Domain Controller VM (DC01) through Remote Desktop. Then, navigate to the local Windows Firewall settings and enable ICMPv4.

6. Return to "Client01" and verify that the ping to "DC01" succeeds. This confirms that the Domain Controller VM (DC01) is properly configured to respond to ping requests, establishing successful connectivity between the client and the Domain Controller.

7. Access "DC01" through Remote Desktop and proceed to install Active Directory Domain Services. This crucial step involves configuring "DC01" as a domain controller, enabling it to manage user accounts, security policies, and domain services within the network environment.

8. While logged into "DC01" via Remote Desktop, proceed with configuring it as a domain controller. During this process, establish a new forest with the domain name "mydomain.com." This step solidifies the network structure, enabling "DC01" to manage user accounts and domain services under the designated domain.

9. After completing the domain controller configuration on "DC01," restart the server. Once it has restarted, log back into "DC01" using the credentials "mydomain.com\labuser." This step ensures that the server is properly rebooted and validates login access for the specified user within the domain environment.

10. Open Active Directory Users and Computers (ADUC) on "DC01." Then, create a new Organizational Unit (OU) named "EMPLOYEES." This OU will serve as a container for organizing user accounts or other objects within the Active Directory domain.

11. Within Active Directory Users and Computers (ADUC) on "DC01," create another Organizational Unit (OU) named "_ADMINS." This OU will be used to group and manage administrative user accounts or other relevant objects within the Active Directory domain.

12. Within the Organizational Unit (OU) named "ADMINS," create a new user account named "Jane Doe" with the username "jane_admin" and assign a password. This account will represent an admin within the domain.

13. Next, add the "jane_admin" account to the "Domain Admins" security group using Active Directory Users and Computers (ADUC). This group membership grants administrative privileges to the user account.

14. Close the Remote Desktop connection to "DC01" and log back in as "mydomain.com\jane_admin." This step ensures that the administrative user account "jane_admin" is properly authenticated and authorized to perform administrative tasks within the domain. Going forward, utilize the "jane_admin" account as the primary administrative account for managing domain resources and performing administrative tasks within the network environment.

15. Access the Azure Portal and navigate to "Client01"'s settings. Update "Client01"'s DNS settings to point to the private IP address of "DC01". Once updated, restart "Client01" from the Azure Portal to apply the changes. This ensures that "Client01" uses "DC01" as its primary DNS server for domain resolution within the network environment.

16. Access Client-1 via Remote Desktop using the original local admin account. Proceed to join "Client01" to the domain. Once joined, "Client01" will automatically restart to finalize the domain joining process.

17. Log in to the Domain Controller via Remote Desktop. Open Active Directory Users and Computers (ADUC) and navigate to the "Computers" container at the root of the domain. Verify that "Client01" appears listed among the domain computers. This confirms successful domain joining and ensures "Client01" is present within the Active Directory domain structure.

18. Log into "Client01" using the "jane_admin" account with "mydomain.com\jane_admin." Once logged in, open the System Properties on "Client01" to verify its domain membership and system configuration.

19. Access the "Remote Desktop" settings on Client01 and configure permissions to allow "domain users" access to remote desktop. This step enables users within the domain to remotely connect to Client01 for administrative or other purposes.
