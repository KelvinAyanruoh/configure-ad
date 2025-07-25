<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

</p>
<p>
Active Directory is an enterprise-level Microsoft tool used to manage  thousands of user accounts and devices in a single place. It also provides ways to manage access control.
</p>
<br />

- Step 1: Create a VM in Azure or using Hyper-V (Windows Server Data Center for AD)
- Step 2: Set up a domain controller IP address static (promote to create a forest)
- Step 3: After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address
- Step 4: Attempt to ping DC-1 private IP address
- step 5: From Client-1, open PowerShell and run ipconfig /all
The output for the DNS settings should show DC-1’s private IP Address



<img width="1031" height="817" alt="image" src="https://github.com/user-attachments/assets/919682fb-df63-4948-b1a7-b729b1608599" />


</p>
<p>
After the VM is created and the DC private IP address is set to static, set Client-1’s DNS settings to DC-1’s Private IP address.
</p>
<br />
<img width="970" height="523" alt="image" src="https://github.com/user-attachments/assets/a56fca75-36e3-4b6b-8f93-554c35216a1e" />
</p>
<p>
Confirm that the ping is successful and run ipconfig /all on client-1. We should then be able to see the DC-1 private IP address in the result, as shown below.
</p>
<br />
<img width="462" height="250" alt="image" src="https://github.com/user-attachments/assets/a52e037b-6ba1-494d-b8b1-639994d702b7" />

<img width="547" height="281" alt="image" src="https://github.com/user-attachments/assets/034b50b8-58d5-49d7-af18-035d4144962f" />


<h2>configuring Active directory in DC-1</h2>

</p>
<p>

</p>
<br />

- Step 1: Go to Server Manager, add Roles and Features 
- Step 2: Check Active Directory Domain Services
- Step 3: After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address
- Step 4: Promote DC-1 to a domain controller


<p>
<img width="849" height="156" alt="image" src="https://github.com/user-attachments/assets/977e440e-e04b-4161-ba24-7b20aa178651" />
<img width="642" height="323" alt="image" src="https://github.com/user-attachments/assets/3c8d509b-a71c-4ac1-b584-dbeeddda8b5f" />
</p>
<p>
<img width="1259" height="929" alt="image" src="https://github.com/user-attachments/assets/4aff35c8-f94e-4ad3-b243-4d96193e8b88" />

<h2>Create a Domain Admin User </h2>

</p>
<p>
Before we create our domain user, we created an Organization Unit. This way we can be able to use this later with our group policies
</p>
<br />


- Step 1: Create two Organization Unit _ADMINS and _EMPLOYEES
- Step 2: Create a Domain user
- Step 3: make the user a Domain admin (and log in to dc-1
- Step 4: Final step, add client-1 to the domain
<p>
<img width="1129" height="509" alt="image" src="https://github.com/user-attachments/assets/a7b05069-9a35-4fd7-85a9-6407da3d9773" />

<img width="1168" height="855" alt="image" src="https://github.com/user-attachments/assets/541051f4-5468-4e11-8433-00a66633153c" />
<img width="618" height="641" alt="image" src="https://github.com/user-attachments/assets/3f241f99-ea51-4c90-8f42-2a052bb7cd75" />
<img width="1175" height="656" alt="image" src="https://github.com/user-attachments/assets/fdaa6cb4-7c60-4d11-96d0-22e5e1d876b0" />





</p>
<p>
The final step will restart your machine. After the restart machine should be in the domain.
</p>
<br />

<h1>Deploy multiple users in AD (Azure)</h1>

- Allow domain users to access the remote desktop
- Log into Client-1 as mydomain.com\jane_admin
- Open system properties
- Click “Remote Desktop”
- Allow “domain users” access to the remote desktop
You can now log into Client-1 as a normal, non-administrative user.



<p>
<img width="966" height="391" alt="image" src="https://github.com/user-attachments/assets/4128b712-8f87-4cdb-a8e2-485fe59ae361" />

</p>
<p>
Login to DC-1 as jane_admin
Open PowerShell_ise as an administrator
Create a new File and paste the contents of the script into it


</p>
<br />
<p>
<img width="1095" height="591" alt="image" src="https://github.com/user-attachments/assets/158622ab-58cd-4a7d-b224-6f37e7a0ee26" />

</p>
<p>
Run the script and observe the accounts being created
When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES)
attempt to log into Client-1 with one of the accounts (take note of the password in the script)

</p>
<br />

</p>
<br />
<p>
<img width="1319" height="589" alt="image" src="https://github.com/user-attachments/assets/cad3a84b-0914-478c-bd9a-ac1f1d839906" />

