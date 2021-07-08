## Active Directory Lab Setup
This guide contains the following:
- [[#Getting Started]]
- [[#Installing Your Virtual Machines]]
- [[#Setting Up Your Intranet]]
- [[#Assigning Your IPs]]
- [[#Installing Active Directory]]
- [[#Active Directory Configuration]]
- [[#Contact me]]

## Getting Started
In this tutorial we're going to set up two virtual machines: A Windows 10 client and Windows Server 2019 running Active Directory. Before we can do that, you'll need copies and a way to virtualize them. It's up to you to decide if you want to implement this lab in the the cloud or on your host machine. I'll only be covering local installation here.

First, you'll need a virtualization program. In this example, we'll be using Virtualbox because of its built-in support for running multiple VMs simultaneously. That said, any virtualzation platform will do. Head over to Virtualbox's website and grab a copy. (https://www.virtualbox.org/)

![[download_vbox.png]]

Next, you can download an image of Server 2019 directly from Microsoft. (https://www.microsoft.com/en-us/windows-server/trial)
You'll be able to install directly from this .iso file.

![[WINserv2019trial.png]]

Finally, you'll need to download the Windows Media Creation tool. (https://www.microsoft.com/en-us/software-download/windows10)
You will have to run this tool to create the boot media for your Windows 10 client.

![[windowsmediacreationtool.png]]

---

## Installing Your Virtual Machines
Once you have your Server 2019 and Windows 10 images, open up Virtualbox and click "New".

![[newVMclickhere.png]]

Select the appropriate options for each VM respectively.

![[newVMnameOS.png|320]] ![[newVMnameOS_2.png|320]]

Give each VM at **least** 2 GBs of memory. The more you can spare, the better, but this is entirely dependent on the limits of your machine.

![[vmMemAssign.png|320]]

Leave the rest of the options default and boot up your machines. You'll be prompted to select the disk images that you previously downloaded and created.

![[selectStartDisk.png|320]]

The rest of this process is just the standard Windows installation and is very straightforward. Login, update, restart, repeat!

#### *Note: Please ensure that you have fully updated your virtual machines before continuing*

---
## Setting Up Your Intranet
Now we're going to put our lab in its own network range. If your VMs are currently active, you will need to shut them off.

Open Virtualbox and select your Windows Server 2019 VM. Then click on **"Settings"**.

![[clickSettings.png]]

Click **"Network"** in the pane on the left then under the **"Attached to:"** drop-down menu, click **"Internal Network"**.

![[selectINTERNALnetwork.png]]

Click the blue arrow next to **"Advanced"** and then under the **"Promiscuous Mode:"** drop-down menu, select **"Allow All"**

![[advancedSETTINGS.png]]

Repeat the above process for your Windows 10 machine.
Start up your VMs as we'll need to manually assign some IP addresses.

---
## Assigning Your IPs

Right click on the **Network** icon in the pane on the bottom-right of your screen and open the **"Network and Internet Settings"**

![[right_click_here.png]]

Click on **"Properties"** under **"Ethernet"**

![[ethernet_properties.png]]

Scroll down to **"Advanced network settings"** and click on **"Change adapter options"** 

![[change_adapt_options.png]]

Right click on your network interface card and select **"Properties"**

![[NIC_properties.png]]

Select **"Internet Protocol Version 4 (TCP/IPv4)"**, then click **"Properties"**

![[ipv4_properties.png]]

Enter in an IP in a private range such a 10.x.x.x, 172.16.x.x, or 192.168.x.x and a subnet mask. I'll be using 10.10.10.10 for my Windows 10 and 10.10.10.19 for my Windows Server 2019 but you can use whatever you would like for your lab.

![[win10ip.png]]

Return to the **"Network and Internet Settings"** window and click **"Network and Sharing Center"**

![[network&sharing.png]]

Click on **"Change advanced sharing settings"**

![[change_adv_share.png]]

Turn on **"network discovery"** and **"file and printer sharing"**

![[netD_FnP.png]]


Repeat this process on your other VM. Make sure your IP addresses are in the same subnet.

![[winservip.png]]

Test for connectivity between your two machines by pinging each other.

![[ping_test.png|450]]


---
## Installing Active Directory

Now that we have our two machines up and running, lets get Active Directory installed. Get started by opening your Windows Server 2019.

Open **"Server Manager"** and then open the **"Add Roles and Features Wizard"**

![[add_roles&features_wiz.png]]

Click **"Next"**

![[clicknextR&Fwiz.png]]

Select **"Role-based or feature-based installation"** and then click **"Next"**

![[RorFthenclick.png]]

Click **"Select a server from the server pool"** and select your Windows Server 2019, then click **"Next"**

![[r&f_serverpool.png]]

In the **"Server Roles"** pane, select the checkbox next to **"Active Directory Domain Services"**

![[r&f_ADDS.png]]

Click **"Add Features"**

![[r&f_add_features.png]]

Click **"Next"**

![[r&f_adds_select.png]]

In the **Features** pane, click **"Next"**

![[r&f_second_next.png]]

In the **AD DS** pane, click **"Next"**

![[ADDS_next.png]]

Finally, click **"Install"**

![[ADDS_install.png]]

---

## Active Directory Configuration
Now that we have *Active Directory Domain Services* installed, a notification will appear prompting you to **"Promote this server to a domain controller"**

![[adds_config_wiz1.png]]

Clicking on **"Promote this server to a domain controller"** will open up the **Active Directory Domain Services Configuration Wizard**.

Select **"Add a new forest"**, give your Root domain a name, and then click **"Next"**

![[adds_config_wiz2.png]]

Enter a password, then click **"Next"**

![[adds_config_wiz3.png]]

Ignore the **"DNS Options"** section, click **"Next"**

![[adds_config_wiz4.png]]

Leave the **"NetBIOS"** name as default, click **"Next"**

![[adds_config_wiz5.png]]

Leave the **"Paths"** as default, click **"Next"**

![[adds_config_wiz6.png]]

Review your choices and click **"Next"**

![[adds_config_wiz7.png]]

If the **Prerequisites Check** throws any errors, correct them, and then click **"Install"**

![[adds_config_wiz8.png]]

After a long process of rebooting and updating, your Windows Server 2019 is configured with Active Directory and is ready to explore!

![[adds_config_wiz9.png]]

Congratulations! You now have an isolated Active Directory Lab! There's so many things you can do with Active Directory. Play around with it! Add users, install and configure SIEMs or EDR tools, load up a Kali Linux VM and add it to your subnet to attack your lab, the possibilities are endless! Have fun and feel free to reach out to me directly if you are having any issues!

## Contact me
Find me at:
- https://linkedin.com/in/kylekingery
- https://github.com/kmc9k1
