<p align="center">
<img src="https://imgur.com/Cj8FV6J.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Network File Shares and Permissions (Azure)</h1>
This tutorial outlines the implementation of Network File Shares and Permissions in an on-premises Active Directory setting within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- File Explorer

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Create some sample file shares with various permissions
</p>
Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
</p>
Connect/log into Client-1 as a normal user (mydomain\<someuser>)
 </p>
On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
 </p>
Set the following permissions (share the folder) for the “Domain Users” group:
 </p>
 Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
  </p>
  <img src="https://imgur.com/nKLLgm9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 </p>
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
 </p>
   </p>
  <img src="[https://imgur.com/kixRIRE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 </p>
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
  </p>
  <img src="[https://imgur.com/r9ZzSxl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 </p>

- Step 2: Attempt to access file shares as a normal user
-  </p>
On Client-1, navigate to the shared folder (start, run, \\dc-1)
  </p>
  <img src="[https://imgur.com/yanqauD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 </p>
Try to access the folders you just created. notice which folders can you access? Which folders can you create stuff in? 
</p>
- Step 3: Create an “ACCOUNTANTS” Security Group, assign permissions, an test access
  </p>
Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”

   </p>
  <img src="[https://imgur.com/ZpMCxSY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 </p>
On the “accounting” folder you created earlier, set the following permissions:
  </p>
Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
  </p>
    <img src="[https://imgur.com/LjI10mE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
  </p>
On Client-1, as  <someuser>, try to access the accountants folder. It should fail. 
   </p>
Log out of Client-1 as  <someuser>
   </p>
On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group
   </p>
  <img src="[https://imgur.com/yanqauD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 </p> 
Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - Does it work now?
  </p>
  <img src="[[hhttps://imgur.com/39SjQ1f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> 
 </p> 
