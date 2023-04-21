<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Protocols and Traffic</h1>

Computer networking: it is how computers communicate with each other. Understanding networking is essential in the field of Information Technology. 

<p></p>

In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.

<p></p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure Virtual Machines
- Microsoft Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create Virtual Machines and Download Wireshark
- Step 2: Observe ICMP Traffic
- Step 3: Observe SSH Traffic
- Step 4: Observe DHCP Traffic
- Step 5: Observe DNS Traffic
- Step 6: Observe RDP Traffic

<h2>Actions and Observations</h2>

<h3>Step 1: Create Virtual Machines</h3>

First step is to create two virtual machines (VMs) in Azure. One VM will be running Windows 10 and the other will be running Linux Ubuntu Server. 

<p></p>

If you need direction how to create VMs in Azure, you can see my tutorial on it [here](https://github.com/tarronacuff/configure-ad).

<p></p>

Once you have created your VMs, log into the Windows VM via Microsoft Remote Desktop. From within the VM, download [Wireshark](https://www.wireshark.org/download.html).

<p>
<a href="https://imgur.com/XwYyqNG"><img src="https://i.imgur.com/XwYyqNG.png" title="source: imgur.com" /></a>
</p>

<p>
<a href="https://imgur.com/DULYE5P"><img src="https://i.imgur.com/DULYE5P.png" title="source: imgur.com" /></a>
</p>

<h3>Step 2: Observe ICMP Traffic</h3>
Next, we'll begin to use Wireshark. Wireshark is a network protocol analyzer and you can use it to observe the capturing of packets from a network connection. Before starting, grab the private Internet Protocol (IP) address of the Linux VM first.

<p>
<a href="https://imgur.com/cKT2sp5"><img src="https://i.imgur.com/cKT2sp5.png" title="source: imgur.com" /></a>
</p>

Internet Control Message Proctol or ICMP is a network protocol that determines if there is communication issues. It is primarily used to report errors. 

<p></p>

Next, open up Wireshark and Windows Powershell. In Wireshark, type in "icmp" in the green bar. In Powershell ping the Linux VM's private IP address (10.0.0.5 in my example). Then ping a public website (Google). Observe the network traffic in both Wireshark and Powershell. Then setup a perpetual ping using "ping -t" + Linux VM's private IP in Powershell. 

<p>
<a href="https://imgur.com/xv9XFHx"><img src="https://i.imgur.com/xv9XFHx.png" title="source: imgur.com" /></a>
</p>

Next, we'll observe what happens when we block the ICMP traffic. Go back to the Linux VM's Azure Portal, then click on Networking. From Networking, click "Add inbound port rule" -> check ICMP -> check Deny, then click "Add". 

<p></p>
This area of Azure is known as Network Security Groups (NSGs). It is basically a firewall in Azure as you can set security rules for your resources. 

<p>
<a href="https://imgur.com/OUznzWd"><img src="https://i.imgur.com/OUznzWd.png" title="source: imgur.com" /></a>
</p>

<p>
<a href="https://imgur.com/e9MVDgp"><img src="https://i.imgur.com/e9MVDgp.png" title="source: imgur.com" /></a>
</p>

<p>
<a href="https://imgur.com/nfKr9Qw"><img src="https://i.imgur.com/nfKr9Qw.png" title="source: imgur.com" /></a>
</p>

<p>
<a href="https://imgur.com/NUQwihf"><img src="https://i.imgur.com/NUQwihf.png" title="source: imgur.com" /></a>
</p>

Once this is done, go back into the Windows VM and observe the changes in Wireshark and Powershell. Since ICMP traffic is being denied, the requests to are timing out and are showing no response.

<p>
<a href="https://imgur.com/BkahGck"><img src="https://i.imgur.com/BkahGck.png" title="source: imgur.com" /></a>
</p>

Next, we'll go back to the Azure Portal and set allow ICMP traffic again. You can either delete the rule or set it to allow. Observe the changes in Wireshark and Powershell again. To stop the perpetual ping, just press "Control" + "C". 

<p>
<a href="https://imgur.com/E4KgenJ"><img src="https://i.imgur.com/E4KgenJ.png" title="source: imgur.com" /></a>
</p>

<p>
<a href="https://imgur.com/SW3qx0e"><img src="https://i.imgur.com/SW3qx0e.png" title="source: imgur.com" /></a>
</p>

<h3>Step 3: Observe SSH Traffic</h3>
Next, we'll observe SSH traffic. Secure Shell Protocol or SSH is a network protocol which allows a secure connection to another machines Command Line Interface (CLI). 

<p> </p>
Filter ssh traffic in Wireshark. Then type "ssh" + the Linux VM's private IP address. Powershell will prompt you to login, so use the Linux VM's login credentials. Once you are logged in via SSH, you can begin to play around with it by using Linux commands such as "cd", "pwd", etc. To exit SSH just type "exit". 

<p>
<a href="https://imgur.com/0OVx8LQ"><img src="https://i.imgur.com/0OVx8LQ.png" title="source: imgur.com" /></a>
</p>

<p>
<a href="https://imgur.com/Lep0TFg"><img src="https://i.imgur.com/Lep0TFg.png" title="source: imgur.com" /></a>
</p>

<h3>Step 4: Observe DHCP Traffic</h3>
Next, we'll observe DHCP traffic. Dynamic Host Configuration Protocol or DHCP is the network protocol responsible for automatically assigning IP addresses.

<p></p>
Filter DHCP traffic in Wireshark. In Powershell, type the command "ipconfig /renew" and observe the changes. 

<p>
<a href="https://imgur.com/nK7aig2"><img src="https://i.imgur.com/nK7aig2.png" title="source: imgur.com" /></a>
</p>

<h3>Step 5: Observe DNS Traffic</h3>
Next, we'll observe DNS traffic. Domain Name System or DNS is the network protocol that transforms Fully Qualified Domain Names (FQDNs) into their assigned IP addresses. Type DNS in Wireshark and the command nslookup. I used Google and Disney in this example. 

<p></p>

If you want to learn about DNS, please see my lab on it [here](https://github.com/tarronacuff/DNS-Tutorial).

<p>
<a href="https://imgur.com/rY6dtUH"><img src="https://i.imgur.com/rY6dtUH.png" title="source: imgur.com" /></a>
</p>

<h3>Step 6: Observe RDP Traffic</h3>
Finally, we'll observe RDP traffic. Remote Desktop Protoctol or RDP is the protocol that allows the remote connection to another computer and complete control of the Graphical User Interface (GUI). Type RDP in Wireshark and observe the traffic. Since it is a VM, you can see there is a lot of RDP traffic. 

<p>
<a href="https://imgur.com/hqNQwBv"><img src="https://i.imgur.com/hqNQwBv.png" title="source: imgur.com" /></a>
</p>

That's it! 
