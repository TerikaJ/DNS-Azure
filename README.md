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

- Windows Server 2022 (Domain Controller - **DC-01**)
- Windows 10 Pro (21H2) (Client - **Client-01**)

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

<h2>Management Steps</h2>

① On the domain controller, change mainframe's record address to 8.8.8.8 (Google) and refresh the DNS server.

② On the client, ping "mainframe"; it will still ping the old IP address.

③ Run ipconfig /displaydns to reveal that the DNS cache still has the old IP.

④ Run ipconfig /flushdns to empty the cache.

⑤ Ping "mainframe" again; the IP address will be updated to the new one on the client side.

⑥ Verify that the new IP address of the record shows when pinging "mainframe".

⑦ Create a CNAME record on the DNS server to point "search" to Google.

⑧ On the Forward Lookup Zones tab in the DNS Manager, open the tab with the domain.

⑨ Create a new CNAME record called "search" and point it to Google.

⑩ Refresh the server to save the changes.

⑪ On the client, ping "search" and use nslookup to return the results of the CNAME record.

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

This project demonstrates the practical application of DNS configuration and management within a domain environment. By creating and updating DNS records, clearing DNS cache, and setting up CNAME records, we have explored how DNS works in real-world scenarios. These exercises underscore the importance of DNS in network communication and provide a hands-on understanding of how to manage DNS settings effectively. Through this project, I have gained valuable experience in configuring and troubleshooting DNS, reinforcing both theoretical knowledge and practical skills essential for IT professionals.

<h1><p align=center> DONE! Good job! </p></h1>

<h2><p align=center>The Next Demonstration:<br><a href="https://github.com/terikaj/FilePermissions-Azure"> Configuring and Managing File Permissions </a></p></h2>

<p align=right>Please delete & clean up your Azure resources when finished!<br>
If you're unsure of how to do this, please click <a href="https://github.com/terikaj/azure-begin">HERE</a>
</p>
