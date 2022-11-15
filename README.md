<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

1. Setup Resources in Azure

    1. Create the Domain Controller VM (Windows Server 2022) named “DC-1”.
   
        a. Take note of the Resource Group and Virtual Network (Vnet) that get created at this time.
        
    2. Set Domain Controller’s NIC Private IP address to be static.
   
        3. Create the Client VM (Windows 10) named “Client-1”. 
    
            - Use the same Resource Group and Vnet that was created in Step 1.a.
   
    4. Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher

        Ensure Connectivity between the client and Domain Controller.

    5. Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping).
   
    6. Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall.
   
    7. Check back at Client-1 to see the ping succeed.

2. Install Active Directory

     8. Login to DC-1 and install Active Directory Domain Services.
   
     9. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is).
   
    10. Restart and then log back into DC-1 as user: mydomain.com\labuser.

3. Create an Admin and Normal User Account in AD

    11. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”.
  
    12. Create a new OU named “_ADMINS”.
  
    13. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”.
  
    14. Add jane_admin to the “Domain Admins” Security Group.
  
    15. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”.
  
    16. User jane_admin as your admin account from now on.


4. Join Client-1 to your domain (mydomain.com)

    17. From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address.
  
    18. From the Azure Portal, restart Client-1.
  
    19. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart).
  
    20. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in ADUC.
  
    21. Create a new OU named “_CLIENTS” and drag Client-1 into there.


5. Setup Remote Desktop for non-administrative users on Client-1

    22. Log into Client-1 as mydomain.com\jane_admin and open system properties.

    23. Click “Remote Desktop”.

    24. Allow “domain users” access to remote desktop.
 
    25. You can now log into Client-1 as a normal, non-administrative user now.
 
    26. Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab).

6. Create a bunch of additional users and attempt to log into client-1 with one of the users.

    27. Login to DC-1 as jane_admin.

    28. Open PowerShell_ise as an administrator.

    29. Create a new File and paste the contents of the script into it. (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

    30. Run the script and observe the accounts being created.
 
    31. When finished, open ADUC and observe the accounts in the appropriate OU.

    32. attempt to log into Client-1 with one of the accounts (take note of the password in the script).


<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/GFiGtmP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/sjYmbFP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>

<h2>Deployment 1</h2>

1. Setup Resources in Azure

    1. Create the Domain Controller VM (Windows Server 2022) named “DC-1”.
   
        a. Take note of the Resource Group and Virtual Network (Vnet) that get created at this time
        
    2. Set Domain Controller’s NIC Private IP address to be static
   
        3. Create the Client VM (Windows 10) named “Client-1”. 
    
            - Use the same Resource Group and Vnet that was created in Step 1.a
   
    4. Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher

        Ensure Connectivity between the client and Domain Controller

    5. Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
   
    6. Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
   
    7. Check back at Client-1 to see the ping succeed

</p>
<br />

<p>
<img src="https://i.imgur.com/EDFW2DA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/6pMwgwX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
    
<h2>Deployment 2</h2>
    
    
2. Install Active Directory

     8. Login to DC-1 and install Active Directory Domain Services.
   
     9. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is).
   
    10. Restart and then log back into DC-1 as user: mydomain.com\labuser .


</p>
<br />

<p>
<img src="https://i.imgur.com/PlD4WJJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/PCebRBU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>

<h2>Deployment 3</h2>    
    
3. Create an Admin and Normal User Account in AD

    11. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
  
    12. Create a new OU named “_ADMINS”
  
    13. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
  
    14. Add jane_admin to the “Domain Admins” Security Group
  
    15. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
  
    16. User jane_admin as your admin account from now on

</p>
<br />

<p>
<img src="https://i.imgur.com/dD0OOvJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/dyBRHvE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>

<h2>Deployment 4</h2>    
    
4. Join Client-1 to your domain (mydomain.com)

    17. From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
  
    18. From the Azure Portal, restart Client-1
  
    19. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
  
    20. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in ADUC
  
    21. Create a new OU named “_CLIENTS” and drag Client-1 into there
    
</p>
<br />

<p>
<img src="https://i.imgur.com/LtXQ5CK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/mTQTZEQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>

<h2>Deployment 5</h2>    
    
5. Setup Remote Desktop for non-administrative users on Client-1

    22. Log into Client-1 as mydomain.com\jane_admin and open system properties

    23. Click “Remote Desktop”

    24. Allow “domain users” access to remote desktop
 
    25. You can now log into Client-1 as a normal, non-administrative user now
 
    26. Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)
    
 </p>
<br />

<p>
<img src="https://i.imgur.com/P4SAquz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/wBXuRRh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>

<h2>Deployment 6</h2>    
    
6. Create a bunch of additional users and attempt to log into client-1 with one of the users

    27. Login to DC-1 as jane_admin

    28. Open PowerShell_ise as an administrator

    29. Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

    30. Run the script and observe the accounts being created
 
    31. When finished, open ADUC and observe the accounts in the appropriate OU

    32. attempt to log into Client-1 with one of the accounts (take note of the password in the script)

 
