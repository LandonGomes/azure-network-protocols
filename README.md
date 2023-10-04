<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1 Create Four seperate folders: Read access, Write access, No access and accounting on the DC-1 VM
- Step 2 Assign permisions for each: Read access (Read only), Write access (write only), No access (read/write Admins only).
- Step 3 Check to verify that the permisions are working as intended to ensure NSG are functioning properly. Create and Organizational unit in Active Directory > New group "ACCOUNTANTS"> add permissions to the accountants> Add members to the Accountants group > go to Client-1 and check and see if the Accounting folder can be accessed > restart client-1 to reboot newly added permissions.
- Step 4 Log into client-1 using the member credentials that was added to the Accountants group > Verify that user can access Accounting folder.

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/L6TNxvE.png"80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  Setting up NSG folders and adding Domain users "read" only, inside DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/Amu2Euh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Setting up NSG folder continued "read/write" only, inside DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/wKTdvYG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Client-1 POV, all four folders that were created in the DC-1 VM are now visible from Client-1 "\\DC-1\.
</p>
<br />

<p>
<img src="https://i.imgur.com/OSkFpoT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Inspecting network traffic from DC-1 to Client-1, as shown in the picture we can determine that the permissions assigned to the no access folder (not granting access to) seems to be functionally as intended.
</p>
<br />

<p>
<img src="https://i.imgur.com/hoCvMWc.png"80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  Upon further investigation of network traffic between DC-1 and Client-1 we can see that the permissions associated with Read Access folder are such that the user can access the folder to read only!!!
</p>
<br />

<p>
<img src="https://i.imgur.com/wKTdvYG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/oriPX0H.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  In the first picture we can see that access was denied to the accounting folder, this was due to the permissions or the lack there of being denied within the DC-1 VM. Admins will need to log into the DC-1 VM and configure the permissions and members for this folder. Once folder configuurations have been implemented, the Client-1 computer will need to restarted as this allows the host added those new permissions to the User account(s).
</p>
<br />
