<h1>DNS Server Configuration and Management 🌐 <h2> 

![how-dns-works](https://github.com/TerikaJ/DNS-Azure/assets/136477450/7cc199b1-53ae-42af-a3d1-2f1a4c122d82)


<h2>Introduction</h2>

In the project, we focus on the practical application of DNS, a fundamental concept in IT. Building on a previous lab where a client VM was joined to the domain VM **'mydomain.com'**, we will configure DNS records and explore their functionality. Logged in as the administrator account **mydomain.com\jane_admin** on both the **Client-01** and **DC-01** VMs, we will demonstrate how DNS operates in a real-world scenario. This hands-on approach emphasizes the importance of administrative access for effective DNS management. 

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows Server 2022 (Domain Controller)
- Windows 10 Pro (21H2) (Client)

<h2>Configuration Steps</h2>


① While logged in to **Client_01** as an administrator (this example uses **mydomain.com\jane_admin**, open the **command prompt**.

<img width="550" alt="1  Open Command Prompt" src="https://github.com/TerikaJ/DNS-Azure/assets/136477450/07b3f3ca-5cb0-4118-b2d5-867791680d7c">

② Ping "mainframe"; it will fail.

<img width="550" alt="2  Ping Mainframe" src="https://github.com/TerikaJ/DNS-Azure/assets/136477450/9a96272f-8e0d-41e4-a6d9-42c0fae38b5e">


③ Use nslookup on "mainframe" to see that there is no DNS record for it.

<img width="550" alt="3  nslookup Mainframe" src="https://github.com/TerikaJ/DNS-Azure/assets/136477450/d5d18e0a-9b80-4b65-a83b-78ca39360cd5">

④ On the ***DC-01**, open the DNS Manager.


⑤ Navigate to your domain within the Forward Lookup Zones tab (e.g., mydomain.com).

⑥ Right-click on the page and select "New Host".

⑦ For the name, input "mainframe" and set the IP address to match the domain controller's IP.

⑧ Refresh the DNS server to update the new record.

⑨ Return to the client and ping "mainframe" again; it should now resolve.


<p>
While logged in to the client as an admin, open the command prompt. When we ping "mainframe" it will fail. Nslookup "mainframe" provides similar results and shows that there is no DNS record for it. A DNS A-record will have to be created for mainframe on the domain controller. On the domain controller, open the DNS Manager and go to the domain you created within the Forward Lookup Zones tab. In my case, it is ernestotest.com. Right click on the page and create a New Host. For name, input mainframe and the IP address should be the same IP as the domain controller so that ping can resolve. Refresh the DNS server so that the new record can be updated. Upon returning to the client, ping mainframe once again to see that it will now resolve.
</p>
<br />

<p>
<img src="https://i.imgur.com/nLlOGKl.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/p0VcajB.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/ds0SCKW.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/d4cXTCS.png" height="80%" width="80%" alt="DNS Steps"/>
</p>
<p>
This next exercise will showcase the DNS cache. On the domain controller, I changed mainframe's record address to 8.8.8.8 (Google) and refreshed the DNS server. When pinging mainframe on the client, it will still ping the old IP address. When the command ipconfig /displaydns is run, it will reveal that the DNS cache still has the old IP. In order to update the cache, we need to clear it. The command ipconfig /flushdns will empty the cache so that when we ping mainframe again, the IP address will be updated to the new one on the client side. When pinging mainframe, the new IP address of the record will show.
</p>
<br />

<p>
<img src="https://i.imgur.com/rI2NYU7.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/FmVM0IU.png" height="80%" width="80%" alt="DNS Steps"/>
<img src="https://i.imgur.com/dyWduSW.png" height="80%" width="80%" alt="DNS Steps"/>
</p>
<p>
A CNAME record will now be made on the DNS server that will point "search" to Google. On the Forward Lookup Zones tab in the DNS Manager, open the tab that has the domain. Create a new CNAME record called search and point it to Google. Refresh the server to save the changes. On the client, pinging search and using nslookup will return the results of the CNAME record.
</p>
<br />

<h2>Conclusion </h2>

This lab made me understand how DNS directly works on a computer and the network. DNS records can change and sometimes this can cause connectivity issues. The DNS cache may have the old records and needs to be cleared out to update to the new records. The ipconfig /flushdns command is a common troubleshooting tool that has been referenced a lot in IT programs and I did not get a complete understanding how and why this works until I have done this lab. In the context of pinging "mainframe" at the start of the lab, the DNS cache gets checked first. If there is no result, the host file will be checked. The DNS server will be checked if there are no results in the host file. I made a record on the DNS server so a ping to mainframe can resolve. A CNAME record maps an alias name to another domain name. In this case, "search" was another name for Google.

<h1><p align=center> DONE! Good job! </p></h1>

<h2><p align=center>The Next Demonstration:<br><a href="https://github.com/terikaj/FilePermissions-Azure"> Configuring and Managing File Permissions </a></p></h2>

<p align=right>Please delete & clean up your Azure resources when finished!<br>
If you're unsure of how to do this, please click <a href="https://github.com/terikaj/azure-begin">HERE</a>
</p>
