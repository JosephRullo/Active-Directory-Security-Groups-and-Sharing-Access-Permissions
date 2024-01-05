<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022

<h2>High-Level Steps</h2>

- Create Sample File Shares with Various Permissions
- Attempt to Access File Shares as a Normal User
- Create a Security Group, Assign Permissions, and Test Access

<h2>Actions and Observations</h2>

** **Note:** ** This demo will utilize the Active Directory installation as well as the Domain Controller and Client Virtual Machines that were created in the previous tutorial. Please view it here for a full walkthrough (https://github.com/JosephRullo/Configuring-Active-Directory-within-Azure-VMs).

<h2>Step 1.</h2>

**Connect/log into the Domain Controller as your Domain Admin Account.** <p> Start by opening up Remote Desktop and connecting to the Domain Controller VM using the Admin account. Open Active Directory Users and Computers -> select a folder where Users are stored, in this example EMPLOYEES (this was the organizational unit that was created in the previous tutorial-see link above) -> select a User and double click -> go to the Account tab -> copy their User logon name. 
<p> 
<p>
<img src="https://i.imgur.com/m0uh01W.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> <img src="https://i.imgur.com/BQGKwCK.png.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> https://i.imgur.com/m0uh01W.png
</p>
<p>
</p>
<br />

<h2>Step 2.</h2> 

**Connect/log into Client as a Normal User.** <p> Now open another session of Remote Desktop and connect to the Client VM -> sign in with the User you just chose from Active Directory.
<p> 
<p>
<img src="https://imgur.com/LstElfn.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/JHjYifD.jpg.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
<br />

<h2>Step 3.</h2> 

**Create Sample Folders From within the Domain Controller.** <p> Back at the Domain Controller VM, from the Start Menu open up the File Explorer -> go to This PC -> select the C: drive -> here right click and create a new folder -> name it READ_ACCESS. Repeat this and create three more folders named: WRITE_ACCESS, NO_ACCESS and ACCOUNTING for this example. Note these folder names are arbitrary and can be whatever you choose.
<p> 
<p>
<img src="https://i.imgur.com/5ce67lp.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 

</p>
<p>
</p>
<br />

<h2>Step 4.</h2> 

**Set Permissions for the “Domain Users” Group:** <p> Let's set the permissions for each of the folders that were just created in the C: drive and share them among the Users in Active Directory. We'll start with the "READ_ACCESS" folder -> right click on it and select "Poperties" -> select the "Sharing" tab -> click "Share" -> type "Domain Users" in the field -> click "Add" (Note the "Permission Level" that is set to the right of "Domain Users". It is set as "Read" this will give the User "Read Only" access aka the access to view the folder and it's contents). -> now click "Share". Next, for the "WRITE_ACCESS" folder right click -> Permissions -> Sharing tab -> click Share -> type Domain Users -> click Add -> this time change the "Permission Level" to "Read/Write" (This will grant the User the ability to not only view the folder, but also the access to "Write" inside of it and add files, change names, etc.) -> click Share. Finally perform the same steps for the NO_ACCESS folder, except add "Domain Admins" instead of "Domain Users" -> Change the Permission Level to "Read/Write" -> Share. (By sharing this NO_ACCESS folder to the Admins, the Users will not have any access to it (either read or write).
<p> 
<p>
<img src="https://i.imgur.com/AIlVHIl.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/i3AYyPR.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
<br />
