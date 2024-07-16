---
layout: post
title: "Part 6 - Active Directory Setup"
categories: Security
parent: Network & Security Home Lab
nav_order: 6
---


## Network & Security Home Lab: 

![banner](/assets/banner.jpg){: width="auto" height="auto" }
###### in progress ***June 24, 2024***

{: .text-center }
### <span style="color: orange; font-weight: bold;">Part 6 - Active Directory Setup</span>

For the  AD (Active Directory) Lab we are going to configure three VMs. We will first configure a Windows Server 2019 first for the DC (Domain Controller) for this machine. The other two VMs will be the clients that use this environment. They will be a Windows 10, and a Windows 11.

Microsoft has provided Evaluation copies for each machine. There is a license period for each, however they should function just fine even after the evaluation period expires. (We can also create snapshots and export copies) The snapshots can be used to roll back to the start of the evaluation period, so it wont expire.

{: .warning}
I will create a video on how to make the AD lab expoitable, and create a Proof-of-Concepts for different attacks. For this guide we will ***only*** be setting up a basic AD configuration and getting a lay of the land.


## <span style="color: royalblue; font-weight: bold;">Downloading Windows ISO Files</span>


### Windows Server 2019

Go to the following link: ***[Windows Server 2019]*** | *Microsoft Evaluation Center*

Click on the `64-bit edition` download. The `.ISO` should be about 5.5GB.

![vbox127](/assets/vbox127.png){: width="auto" height="auto" }

### Windows 11 Enterprise

Go to the following link: ***[Windows 11 Enterprise]*** | *Microsoft Evaluation Center*

Click on the `64-bit edition` download. The `.ISO` should be about 6GB.


![vbox128](/assets/vbox128.png){: width="auto" height="auto" }

### Windows 10 Enterprise

Go to the following link: ***[Windows 10 Enterprise]*** | *Microsoft Evaluation Center*

Click on the `64-bit edition` download. The `.ISO` should be about 4GB.

![vbox129](/assets/vbox129.png){: width="auto" height="auto" }



### ISO File Names

```scss
ISO Name	OS Name
17763.3650.221105-1748.rs5_release_svc_refresh_SERVER_EVAL_x64FRE_en-us	`Windows Server 2019`
22631.2428.231001-0608.23H2_NI_RELEASE_SVC_REFRESH_CLIENTENTERPRISEEVAL_OEMRET_x64FRE_en-us `Windows 11 Enterprise`
19045.2006.220908-0225.22h2_release_svc_refresh_CLIENTENTERPRISEEVAL_OEMRET_x64FRE_en-us	`Windows 10 Enterprise`

```

The build number and file names may slightly differ.

> Make sure to rename the files with an identifiable name in order to mitigate user error.

![vbox130](/assets/vbox130.png){: width="auto" height="auto" }

### <span style="color: royalblue; font-weight: bold;">Creating the VMs</span>


### Windows Server 2019

Click on Tools from the VirtualBox sidebar and select New.

![vbox131](/assets/vbox131.png){: width="auto" height="auto" }

Gave the VM a name. Ensure that the Folder option points to the location where all the Home Lab-related VMs are saved. For the ISO Image select the downloaded Windows Server 2019 image. Select the `Skip Unattended Installation` option and then click on `Next`.

Increase the Memory to `4096MB` and click on `Next`.

Increase the Hard Drive size to `100GB` and then click on `Next`.

Confirm that all the values look correct and then click on `Finish`.

![vbox132](/assets/vbox132.png){: width="auto" height="auto" }

---- 

![vbox133](/assets/vbox133.png){: width="auto" height="auto" }

{: .new}
The next VirtualBox installation of the Windows 11 VM, and Windows 10 VM will be very similar. I put dropdown refrence images to save space if they are needed.

## <span style="color: royalblue; font-weight: bold;">Windows 11 Enterprise VM</span>

From the VirtualBox sidebar select Tools and then click on `New`.

Give the VM a name. Ensure that the Folder option is pointing to the location where all the Home Lab VMs are saved. For the ISO Image option select the Windows 10 Enterprise image. Tick the `Skip Unattended Installation` option. Click on `Next` to continue.

Leave Memory and CPU on its default value. Click on `Next`.

Increase the Hard Disk size to `80GB` and then click on `Next`.

Verify that all the options are correct and then click on `Finish`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox135](/assets/vbox135.png){: width="auto" height="auto" }
![vbox136](/assets/vbox136.png){: width="auto" height="auto" }
</details>

## <span style="color: royalblue; font-weight: bold;">Windows 10 Enterprise VM</span>

Follow the same steps as above to create the VM for the second AD user.

{: .warning}
You can allocate more cores or resources if there is issues with Virtualization of the Windows Operating sytems.

### Adding all of the VMs to a Group

Right-click on the Windows Server 2019 VM, Windows 11, and Windows 10 then choose `Move to Group` -> [New].

Right-click on the group name and select `Rename Group`. Name the group `Active Directory`.

Right-click on the group name (Active Directory) and choose `Move to Group` -> `Home Lab`.

The final output should look as follows:

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox134.png](/assets/vbox134.png){: width="auto" height="auto" }

</details>

## <span style="color: royalblue; font-weight: bold;">Configuring the VMs</span>

{: .new}
Again, the next VirtualBox configuration steps of the Windows Server 2019, Windows 11 VM, and Windows 10 VM will be very similar. I put dropdown refrence images to save space if they are needed.

### <span style="color: royalblue; font-weight: bold;">Windows Server 2019 </span>

Select the Windows Server 2019 VM and click on `Settings` from the toolbar.

Go to `System` -> `Motherboard`. For Boot Order ensure Hard Disk is not the top followed by `Optical`. Disable `Floppy`.

Go to `Network` -> `Adapter 1`. For the Attacked to field select Internal Network. For name select `LAN 2`. Click on `OK` to save the settings.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox137.png](/assets/vbox137.png){: width="auto" height="auto" }
![vbox138.png](/assets/vbox138.png){: width="auto" height="auto" }
![vbox139.png](/assets/vbox139.png){: width="auto" height="auto" }

</details>

### <span style="color: royalblue; font-weight: bold;">Windows 11 Enterprise </span>

Select Windows 11 Enterprise from the sidebar and then from the toolbar choose Settings.

Go to `System` -> `Motherboard`. For Boot Order ensure Hard Disk is on the top followed by `Optical`. Disable `Floppy`.

Go to `Network` -> `Adapter 1`. For the Attacked to field select `Internal Network`. For name select `LAN 2`. Click on `OK` to save the settings.

### <span style="color: royalblue; font-weight: bold;">Windows 10 Enterprise </span>

Select Windows 10 Enterprise from the sidebar and then from the toolbar choose `Settings`.

Go to `System` -> `Motherboard`. For Boot Order ensure `Hard Disk` is on the top followed by `Optical`. Disable `Floppy`.

Go to `Network` -> `Adapter 1`. For the Attacked to field select Internal Network. For name select `LAN 2`. Click on `OK` to save the settings.

----


## <span style="color: royalblue; font-weight: bold;">Windows Server 2019 Setup</span>


### OS Installation

Select Windows Server 2019 from the sidebar and click on `Start` from the toolbar.

Click on `Next`.

Click on Install now.

Select `Windows Server 2019 Standalone Evaluation (Desktop Experience)` and click on `Next`.

Accept the agreement and click on `Next`.

Select `Custom: Install Windows only (Advanced)`.

Select `Disk 0` and click on `Next`.

The VM will restart a couple of times during the installation process.

{: .new}
For the Installation of the Windows Server, refer to the below pictures.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox140.png](/assets/vbox140.png){: width="auto" height="auto" }
![vbox141.png](/assets/vbox141.png){: width="auto" height="auto" }
![vbox142.png](/assets/vbox142.png){: width="auto" height="auto" }
![vbox143.png](/assets/vbox143.png){: width="auto" height="auto" }
![vbox144.png](/assets/vbox144.png){: width="auto" height="auto" }
![vbox145.png](/assets/vbox145.png){: width="auto" height="auto" }
![vbox146.png](/assets/vbox146.png){: width="auto" height="auto" }
![vbox147.png](/assets/vbox147.png){: width="auto" height="auto" }

</details>

## <span style="color: royalblue; font-weight: bold;">OS Setup & Configuration</span>  10:37

Once the installation is complete,

> Enter a password for the Administrator account. Once set and remembered click on `Finish`.

![vbox148.png](/assets/vbox148.png){: width="auto" height="auto" }


Once at the login Screen we can use the `Ctrl+Alt+Delete` shortcut.

![vbox149.png](/assets/vbox149.png){: width="auto" height="auto" }

Once we log in. Server Manager will automatically open. A popup will also open asking us to try Windows Admin Center. Click on Don't show this message again and then click on X to close the popup.

![vbox150.png](/assets/vbox150.png){: width="auto" height="auto" }

### Guest Additions Installation

To make the Virtual machine autosize the window we need to install Guest Additions. From the VM toolbar click on `Devices` -> `Optical Devices` -> `Remove disk` from virtual drive. This will remove the `Windows Server 2019 image` from the disk drive.


![vbox151.png](/assets/vbox151.png){: width="auto" height="auto" }


Then select `Devices`-> `Insert Guest Additions CD image`.

![vbox152.png](/assets/vbox152.png){: width="auto" height="auto" }

From the taskbar open File Explorer. Once the disk is loaded it will show up in the sidebar. Click on it to view its content. Double-click on VBoxWindowsAdditions (4th file from bottom) to start the installer.

Click on `Next`.

Click on `Next`.

Click on `Next` again to install the requirement components.

Choose `Reboot now` and click on `Finish`. The VM will restart automatically.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox154.png](/assets/vbox154.png){: width="auto" height="auto" }
![vbox155.png](/assets/vbox155.png){: width="auto" height="auto" }
![vbox156.png](/assets/vbox156.png){: width="auto" height="auto" }

</details>


> After restarting, log in. 

> From the VM toolbar click on `Devices` -> `Optical Drivers` -> `Remove disk` from virtual drive to remove the Guest Additions image.

![vbox157.png](/assets/vbox157.png){: width="auto" height="auto" }

Now we have more functionality for resizing the screen.

> Use the shortcut `Right Ctrl+F` to enter and exit Fullscreen mode. 

## <span style="color: royalblue; font-weight: bold;">Network Configuration</span>

During the pfSense setup module (Part 2) we disabled `DHCP` on the `AD_LAB` interface and now out Windows Server will *not* automatically be assigned an IP address. We intentionally set it up this way because we want to create a Domain Controller with other machines attached.

From the taskbar right-click on the network icon and select Open `Network & Internet settings`.

![vbox158.png](/assets/vbox158.png){: width="auto" height="auto" }

Click on “Change adapter options”.

On the Network Connections page, we should see the `Ethernet adapter`. Right-click on the adapter and select `Properties`.

Select `Internet Protocol Version 4 (TCP/IPv4)` and click on `Properties`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox159.png](/assets/vbox159.png){: width="auto" height="auto" }
![vbox160.png](/assets/vbox160.png){: width="auto" height="auto" }
![vbox161.png](/assets/vbox161.png){: width="auto" height="auto" }


</details>


> Once in the IPV4 Properties

Enter the details as shown below and then click on `OK`. Click on `OK` again to close the Ethernet Properties menu.

IP address: `10.80.80.2`
Subnet mask: `255.255.255.0`
Default gateway: `10.80.80.1`
Preferred DNS Server: `10.80.80.2`

> Double check below

![vbox162.png](/assets/vbox162.png){: width="auto" height="auto" }

> Next, Windows will display a notification to allow internet access click on Yes.

![vbox163.png](/assets/vbox163.png){: width="auto" height="auto" }

21:22

Close the Network Connections page.

In the Settings app click on the Home button (above search bar).

Renaming the System

Before we can set up the machine to be a Domain Controller let us rename the PC. Select “System”.

Click on About on the sidebar and then click on the “Rename this PC” button. Give the PC an easy-to-remember name and then click on Next.

Click on “Restart now” for the changes to take effect.

## <span style="color: royalblue; font-weight: bold;">Active Directory & DNS Installation</span>

After login wait for Server Manager to load. Click on the Manage button from the top right corner and select “Add Roles and Features”.

Click on Next till you reach the Server Roles page.

On this page enable “Active Directory Domain Services” and “DNS Server”.

When you enable a feature the “Add Roles and Features Wizard” will open click on “Add Features” to confirm the selection.

Once both the features are selected click on Next to proceed with installation.

Click Next till you reach the Confirmation page. Here click on Install to start the installation of the selected features.

Once the installation is complete click on Close to exit the Wizard.\

## <span style="color: royalblue; font-weight: bold;">Active Directory Configuration</span>

Click on the Flag icon present in the top right of the toolbar in Server Manager. From the dropdown click on “Promote this server to a domain controller”.

The AD Domain Servers Configuration Wizard will open. For deployment operation select Add a new Forest. Give the domain a name. For my setup, I will be using the domain name ad.lab. After selecting the name click on Next.

    The name assigned to the domain has to be made of two words that are separated by a period.

On this page enter a password to use for using the AD Restore feature.

Ignore the warning that is shown and click on Next.

The NetBIOS name should automatically be filled. It will be the first part of the domain name. Click on Next to continue.

Click on Next.

Click on Next.

Click on Install to start the Domain Services setup process.

Once the install process is complete the machine will need to restart. Click on Close to reboot the system.

On restart, you will notice that the name that is shown on the login page has changed. The first part of the domain name is prepended to the username. This means the machine has successfully been configured as the domain controller. Log in using the Administrator password.

### <span style="color: royalblue; font-weight: bold;">DNS Configuration</span>

Since we enabled DNS on this machine (Domain Controller). This machine (DC) will act as the DNS server for devices that are connected to the ad.lab environment. For the DNS service to function properly we need to configure a Forwarder. Forwarder is the device to which the DNS queries will be sent when the DC cannot resolve it. In our case, we need to forward the request to pfSense. The DNS service of pfSense will then perform the lookup.

Open the Start menu expand the “Windows Administrative Tools” folder and select DNS.

In the sidebar select the Domain Controller (in my case DC1) and from the right menu double-click on “Forwarders”.

Go to Forwarders -> Edit.

This will open the Forwarder configuration page. Enter the IP address of the AD_LAB interface (10.80.80.1) and press Enter.

Once added. Click on OK to confirm the change.

Click on Apply then OK to save the changes.

### <span style="color: royalblue; font-weight: bold;">DHCP Installation</span>

Since DHCP is disabled on the AD_LAB interface when new devices are added they will not be assigned an IP address. We will enable the DHCP service on the DC. Once set devices that connect to the AD_LAB network will be automatically assigned an IP address by the Domain Controller DHCP server.

Click on Manage from the toolbar in Server Manager. Then choose “Add Roles and Features”.

Keep clicking Next till you reach the “Server Roles” page. Enable “DHCP Server” then click on “Add Features”.

Keep clicking Next till you reach the Confirmation page. Click Install to enable DHCP.

### <span style="color: royalblue; font-weight: bold;">DHCP Configuration</span>

After the installation is complete click on the Flag present in the toolbar of Server Manager and click on “Complete DHCP configuration”.

Click on Commit.

Click on Close to complete the installation.

From the Start menu click on “Windows Administrative Tools” and then choose DHCP.

Expand the DHCP server (in my case dc1.ad.lab) dropdown on the left side of the window.

Right-click on IPv4. Then select “New Scope”. The scope defines the range of IP addresses that can be assigned to devices by the DHCP server.

Enter a Name and Description for the new scope.

Enter the details as shown below.

Start IP address: 10.80.80.11
End IP address: 10.80.80.253
Length: 24
Subnet mask: 255.255.255.0

    You can chose the Start IP address to be 10.80.80.3. I have purposely left the starting IP addresses out of the DHCP scope. In the future if the need arises I can use these IPs for static IP assignment.

We don’t have any Exclusions (static IP assignment). Leave all the options empty and click on Next.

Increase the lease time to 365 days and click on Next.

    Since we increased the lease duration when a IP address is assigned to a device the device will be allowed to use that IP address without requesting a new IP address for 365 days.

Select “Yes, I want to configure these options now” and click on Next.

In the IP address field enter the default gateway for the AD_LAB interface (10.80.80.1) and then click on Add. Once added click on Next.

Click on Next.

We are not configuring a WINS Server for our environment so click on Next.

Select “Yes, I want to activate this scope now” and click on Next.

So far we have installed Windows Server 2019, installed Guest Additions, configured the VM to be the Domain Controller (DC), set up a DNS Forwarder and configured DHCP. We still need to create users in the DC and set up client machines to use the AD environment. We will cover these topics in part 2 of this module.

<span style="color: royalblue; font-weight: bold;">Part 7 - Active Directory Lab Setup - Part 2</span> 


[Windows Server 2019]: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019

[Windows 11 Enterprise]: https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise

[Windows 10 Enterprise]: https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise