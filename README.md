<p align="center">
<img src="https://github.com/ColtonTrauCC/network-fileshare/assets/147654000/efe94bff-a469-4342-a4c6-e927befd13b9" height = 20% width = 20%/>
</p>

<h1 align = "center">Network Fileshare and Permissions</h1>
File sharing and permissions set up is a structure in order to organize resources and make sure users have the appropriate permissions and access to files they need.
<br />

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Remote Desktop</li>
  <li>Active Directory Domain Services</li>
</ul>

<br />

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2022</li>
  <li>Windows 10 Pro (21H2)</li>
</ul>

<br />

<h2>Steps</h2>

<h3>Create some sample file shares with various permissions</h3>

</p>
Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin) - Connect/log into Client-1 as a normal user (mydomain\<someuser>)
</p>
On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
<p>

<b>read-access</b>: Set the following permissions (share the folder) for the “Domain Users” group by hitting “properties> sharing”
</li>
<p>
<b>write-access</b>: Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
</li>
<p>
<b>no-access</b>: Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
</li>
<p>
<b>accounting</b>: Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write” - (Skip accounting for now)
</li>
<p>
An Example of setting group and permissions
<p>
<img src="https://i.imgur.com/ndNuGdF.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
</p>

<br/>

<h3>Attempt to access file shares as a normal user</h3>

<p>
On Client-1, navigate to the shared folder (start, run, \\dc-1)
<p>
Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in?
<p>
<img src="https://i.imgur.com/JS9i56l.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>

<br/>

<h3>Creating a Security Group</h3>

<p>
Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS” (“New organizational unit in AD”)
<p>
<img src="https://i.imgur.com/jU71aqY.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
On the “accounting” folder you created earlier, set the following permissions - Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
<p>
<img src="https://i.imgur.com/ndNuGdF.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
On Client-1, as  <someuser>, try to access the accountants folder. It should fail. since its not part of the group. Log off and remember the username that was used to log into the Client, its going to be set as part of the accountants group
<p>
Log out of Client-1 as  <someuser> and on DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group
<p>
<img src="https://i.imgur.com/yejapaP.jpg" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - It should work now
<p>
This is the end of the lab
