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

**Create Sample Folders From within the Domain Controller.** <p> Back at the Domain Controller VM, from the Start Menu open up the File Explorer -> go to This PC -> select the C: drive -> here right click and create a new folder -> name it READ_ACCESS. Repeat this and create three more folders named: WRITE_ACCESS NO_ACCESS and ACCOUNTING for this example. Note these folder names are arbitrary and can be whatever you choose.
<p> 
<p>
<img src="https://i.imgur.com/SaLlHNr.png." height="60%" width="60%" alt="Disk Sanitization Steps"/> 
<img src="https://i.imgur.com/JHjYifD.jpg.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
<br />
