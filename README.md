<p align="center">
<img src="https://i.imgur.com/GqnCLgU.jpeg" alt="Domain Name System and IP" height="80%" width="80%"/>
</p>

<h1>Using a Domain Controller VM and Client VM for DNS Exploration</h1>
This will be a quick showcasing of Domain Name Systems within Azure Virtual Machines.<br />
<br></br> 
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
  
<br></br>
<h2>First, </h2>

- Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
  
- Connect/log into Client-1 as an admin (mydomain\jane_admin)
<img src="https://i.imgur.com/gBX1Vpp.png" height="80%" width="80%">

- From Client-1, try to ping “mainframe”. Notice that it fails
  
- Nslookup “mainframe” notice that it fails (no DNS record)
  
<img src="https://i.imgur.com/WmjBTkV.png" height="80%" width="80%"> 

- Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address

<img src="https://i.imgur.com/QHKgdti.png" height="80%" width="80%">

- Go back to Client-1 and try to ping it. Observe that it works

<img src="https://i.imgur.com/D7f7NHv.png" height="80%" width="80%">
<br></br> 
<h4 align="center"> DNS Cache Exercise </h4>

- Go back to DC-1 and change mainframe’s record address to 8.8.8.8

<img src="https://i.imgur.com/JeJMI14.png" height="80%" width="80%">

- Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address

<img src="https://i.imgur.com/Loaa8Cv.png" height="80%" width="80%">

- Observe the local DNS cache (ipconfig /displaydns) 

<img src="https://i.imgur.com/rhlkThc.png" height="80%" width="80%">

- Flush the DNS cache (ipconfig /flushdns).
  
- Observe that the cache is empty (ipconfig /displaydns)

- Attempt to ping “mainframe” again. Observe that the address of the new record is showing up

<img src="https://i.imgur.com/HRnct3G.png" height="80%" width="80%"> 
<br></br> 

<h4 align="center"> CNAME Record Exercise </h4>

- Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com”
  
<img src="https://i.imgur.com/WDCeNBW.png" height="80%" width="80%">

- Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record 

<img src="https://i.imgur.com/Z6S0f4W.png" height="80%" width="80%"> 

- On Client-1, nslookup “search”, observe the results of the CNAME record

<img src="https://i.imgur.com/fqyLywU.png" height="80%" width="80%">

<p align="center"> Creating a CNAME record (short for Canonical Name) tells the internet that one domain name is just another name for a different domain. This helps to avoid duplicating IP addresses and makes other subdomains of services easier to manage like blogs.  </p>

<h5 align="center"> End of Showcase </h5>
