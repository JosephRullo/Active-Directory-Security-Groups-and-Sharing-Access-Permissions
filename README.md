<p align="center">
<img src="https://i.imgur.com/Q0kMemE.jpg" height=120% width=120% alt="ANSG"/>
</p>

<h1> <p align="center"> Network Security Groups (NSGs) and Sharing Access Between Azure Virtual Machines</h1>
<p align="center"> In this tutorial, we observe sharing access to folders to and from Azure Virtual Machines as well as experiment with Network Security Groups. <br />
<br />
<br /> 
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022

<h2>High-Level Steps</h2>

- Create Sample File Shares with Various Permissions
- Attempt to Access File Shares as a Normal User
- Create a Security Group, Assign Permissions, and Test Access

<h2>Actions and Observations</h2>

** **Note:** ** This demo will utilize the Active Directory installation as well as the Domain Controller and Client Virtual Machines that were created in the previous tutorial. Please view it here for a full walkthrough.
<p>
(https://github.com/JosephRullo/Configuring-Active-Directory-within-Azure-VMs).

<h2>Step 1.</h2>

**Connect/log into the Domain Controller as your Domain Admin Account.** <p> Start by opening up Remote Desktop and connecting to the Domain Controller VM using the Admin account.
<p> 
<p>
<img src="https://i.imgur.com/tlCbzyo.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2>Step 2.</h2>

**Choose a User in Active Directory.** <p> Open Active Directory Users and Computers -> select the folder where Users are stored, in this example EMPLOYEES (this was the organizational unit that was created in the previous tutorial-see link above) -> select a User and double click -> go to the Account tab -> copy their User logon name and paswword.
<p> 
<p>
<img src="https://i.imgur.com/bCFjjgF.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2>Step 3.</h2> 

**Connect/log into Client as a Normal User.** <p> Now open another session of Remote Desktop and connect to the Client VM -> sign in with the User you just chose from Active Directory.
<p> 
<p>
<img src="https://i.imgur.com/T2CUyvo.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/JHjYifD.jpg.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
<br />

<h2>Step 4.</h2> 

**Create Sample Folders From within the Domain Controller.** <p> Back at the Domain Controller VM, from the Start Menu open up the File Explorer -> go to This PC -> select the C: drive -> here right click and create a new folder -> name it READ_ACCESS. Repeat this and create three more folders named: WRITE_ACCESS, NO_ACCESS and ACCOUNTING for this example. Note these folder names are arbitrary and can be whatever you choose.
<p> 
<p>
<img src="https://i.imgur.com/k9QolOu.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2>Step 5.</h2> 

**Set Sharing Permissions for the “Domain Users” Group.** <p> Let's set the permissions for each of the folders that were just created in the C: drive and share them among the Users in Active Directory. We'll start with the "READ_ACCESS" folder -> right click on it and select "Poperties" -> select the "Sharing" tab -> click "Share" -> type "Domain Users" in the field -> click "Add" (Note the "Permission Level" that is set to the right of "Domain Users" is set as "Read". This will give the User "Read Only" access, the permission to view the folder and it's contents without the ability to modify them in any way). -> now click "Share". After clicking share, a pop up window will appear showing the path to this folder within the Domain Controller. Copy this path as we will need it in the coming steps. Next up, for the "WRITE_ACCESS" folder right click -> Permissions -> Sharing tab -> click Share -> type Domain Users -> click Add -> this time change the "Permission Level" to "Read/Write" (This will grant the User the access to not only view the folder, but also the permission to "Write" inside of it and add files, change names, etc.) -> click Share.
<p> 
<p>
<img src="https://i.imgur.com/4qqZtr9.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/r8oDATM.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/CWVvQTk.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2>Step 6.</h2> 

**Set Sharing Permissions for the “Domain Users” Group (continued).** <p> Finally perform the same steps for the NO_ACCESS folder, except this time type "Domain Admins" in the field 
-> click Add -> Change the Permission Level to "Read/Write" -> Share. (By sharing this NO_ACCESS folder to the Domain Admins only, the Users will not have any access to it (either read or write). Let's leave the "ACCOUNTING" folder as is for now, we will set different permissions for that in the coming steps.
<p> 
<p>
<img src="https://i.imgur.com/IgDg4Fk.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2>Step 7.</h2> 

**Attempt to Access File Shares as a Normal User.** <p> Switching back to the Client VM signed in as a User (In this example Alice. A from the EMPLOYEES group) open the File Explorer and enter the folder path that was copied in the above step. You should now see the three folders that we shared access with in the Domain Controller. Double click on the READ_ACCESS folder, you will notice you can open and view it. However try to right click -> select new -> folder  (Notice you will get a "Access Denied" message)
<p> 
<p>
<img src="https://i.imgur.com/SQQqhcX.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/xYJ49ir.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/cPBDQmU.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<p>
</p>
<br />

<h2>Step 8.</h2> 

**Attempt to Access File Shares as a Normal User (continued).** <p> Now go back and double click the WRITE_ACCESS folder. After it opens, right click and try to add a new folder (for example Documents). This time you'll notice that you can create a new folder since you were given "Write" permission. This folder will now appear in the Domain Controller in the C: drive within the WRITE_ACCESS folder as you would expect (you can briefly switch back to the Domain VM and observe the change).
<p> 
<p>
<img src="https://i.imgur.com/380MIwB.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/PVxUoiI.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2>Step 9.</h2> 

**Attempt to Access File Shares as a Normal User (continued).** <p> Lastly on the Client VM, go back and try to open the NO_ACCESS folder. Again you will receive a "Access Denied" message stating you do not have permission to view it. You would need to logoff and logon as the Domain Admin to gain access to this folder. Give it a test.
<p> 
<p>
<img src="https://i.imgur.com/0RIZ6fV.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
<br />

<h2>Step 10.</h2> 

**Create a Security Group.** <p> Moving back to the Domain Controller VM, open Active Directory Users and Computers -> right click on your domain -> select new -> select organizational unit -> name it (for this example SECURITY GROUPS). Now right click on this new unit -> select New -> select Group -> assign it a name (in this example ACCOUNTANTS) -> check the "Security" button under "Group Type" -> click Ok.
<p> 
<p>
<img src="https://i.imgur.com/4XrbdIr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2>Step 11.</h2> 

**Assign Sharing Permissions to Security Group.** <p> Open File Explorer and go to the C: drive -> right click on the ACCOUNTING folder -> select Properties -> click the Sharing tab -> click Share -> type the name of the Security Group (ex. ACCOUNTANTS) you created and click Add -> grant Read/Write access under Permission Level -> click Share -> click done.
<p> 
<p>
<img src="https://i.imgur.com/PVvPGZA.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/Ln0ykSs.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<p>
</p>
<br />

<h2>Step 12.</h2> 

**Assign a Member to the Security Group.** <p> No one has access to this Security Group just yet, because we have not added any members to it. Let's do that now, first choose which User you will make a member of the Security Group (for this example someone from EMPLOYEES). Now go back to Active Directory Users and Computers -> go to the SECURITY GROUPS unit -> double click on ACCOUNTANTS group -> select the Members tab -> click Add -> type in the bottom field the name of the User you chose (for this example Grace. G) -> click Check Names -> click Ok -> click Apply -> click Ok.
<p> 
<p>
<img src="https://i.imgur.com/xFEJOhK.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/BzgPCj9.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2>Step 13.</h2> 

**Test Access.** <p> Now switch back to the Client VM and logoff (you must logoff and logon again to have these permissions take effect.) Log back on to the Client VM as the User you selected as a member of the Security Group -> open File Explorer -> go to the Domain path with the ACCOUNTING folder and try to open it and and create a new folder in it (ex. Receipts). No error messages should appear. Switch back to the Domain Controller VM and confirm that the new folder was created here as well. 
<p> 
<p>
<img src="https://i.imgur.com/2seg6vF.png" height="40%" width="40%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/bj2Hi4V.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/q8OlhnP.png" height="60%" width="60%" alt="Disk Sanitization Steps"/> 
</p>
<p>
</p>
<br />

<h2> <p align="center"> This Concludes the Network Security Group Sharing Tutorial. </h2>
