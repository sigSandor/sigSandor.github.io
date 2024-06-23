---
layout: post
title: "Part 2 - pfSense Setup & Configuration"
categories: Security
parent: Network & Security Home Lab
nav_order: 2
nav_exclude: false

---

{: .text-center }
# Network & Security Home Lab: 

{: .text-center }
## <span style="color: orange; font-weight: bold;">Part 2 - pfSense initial Setup & Configuration</span>

![banner](/assets/banner.jpg){: width="auto" height="auto" }

###### Posted ***May 22, 2024***



In this module, we will go over the basic installation of ***pfSense***. Additionally, we will also complete the system configuration, and network interfaces for our lab.

----

{: .warning }
pfSense is going to be the default gateway and firewall for our home lab. 
This means that pfSense should be the first VM that is booted. 
Once pfSense is launched other VMs in the lab can be launched following.

## Downloading pfSense

Go to the page : `pfSense Community Edition` > [Download] 

As of May 22, 2024 the latest version of pfSense is `2.7.2`.

You will most likely have to create an account with NetGate, who is partnered with pfSense.
Account setup is *free*, but will require some self navigation to access the download.

![vbox18.png](/assets/vbox18.png){: width="auto" height="auto" }

### Select an option with the following:

> Architecture: `AMD64 (64-bit)`

> Installer: `DVD Image (ISO) Installer`

> Mirror: `Location closest to you`

The downloaded file should have the extension of `.iso.gz`

You can use *7-Zip* or another decompression software to extract the image.

After extraction, we should have a file that has the `.iso` extension. 


> Optionally, you can move the ISO to a new directory in which you will be storing your lab iso. 
 
![vbox19.png](/assets/vbox19.png){: width="auto" height="auto" }


## pfSense VM Creation

Launch VirtualBox. Click on `Tools` from the sidebar and then ***New***.


> For name selection, PfSense is fine. 
> The Folder option defines the location where the VM will be saved (I created a new folder called VirtualBox VMs)

> From the ISO Image dropdown select *Others* in oreder to select the .iso file that we just extracted. 
> Select Type as `BSD` and Version as `FreeBSD (64-bit)` and then click on `Next`.

![vbox3](/assets/vbox3.png){: width="auto" height="auto" }

On the next page, we can select the amount of RAM and CPU that the VM can use. As a Baseline, You can choose 1024-2048 Base memory and 1-2 CPU cores. Click on `Next` to continue. 
> (No need for extraneous Memory or Enabling EFI)


![vbox4](/assets/vbox4.png){: width="auto" height="auto" }

On the next page, we can choose the amount of storage space to reserve for the VM. 20GB is just fine for this less resource heavy VM.

![vbox5](/assets/vbox5.png){: width="auto" height="auto" }


## Final Confirmation

![vbox6](/assets/vbox6.png){: width="auto" height="auto" }
 > Confirm that everything looks right and then click on `Finish`.
 > Once done we should see the newly created VM in the sidebar.
 

## Grouping our First VM

I want to keep the VMs organized by using the Groups feature of VirtualBox. I would strongly suggest implementing organization since we are dealing with a large number of virtual machines.

> To Create a group

Right-click on the pfSense VM from the sidebar, `select Move to Group -> *New*`. The VM will now be added to a Group called New Group.

Right-click on the Group, and select `Rename Group`. Name the Group ***Firewall***.

The final result should match the following:

![vbox7](/assets/vbox7.png){: width="auto" height="auto" }

## pfSense Basic Virtual Configuration

Before we boot the VM we need to configure some settings related to VirtualBox. Select the pfSense VM from the sidebar and then click on `Settings`.

![vbox20.png](/assets/vbox20.png){: width="auto" height="auto" }

## System Configuration

Select `System -> Motherboard` in the Boot Order section use the arrows to move `the Hard Disk` to the top, `Optical` should be next. Ensure that `Floppy` is unchecked.

![vbox21.png](/assets/vbox21.png){: width="auto" height="auto" }

{: .warning }
You may have to drag the top of the window *upwards* in order to hit the next button.

### Audio & USB Configuration

> Go to the Audio tab and disable Audio option. Since the VM we are configuring is a router we will not be using audio. (optional)


> Go to the USB tab and uncheck the Enable USB Controller option. Since this VM we are configuring is a router we will not need USB support. (optional)

## Network Configuration

Go to `Network -> Adapter 1`. For the Attached to field select `NAT`. Expand the `Advanced` section and for Adaptor Type select `Paravirtualized Network (virtio-net)`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox22.png](/assets/vbox22.png){: width="auto" height="auto" }
![vbox23.png](/assets/vbox23.png){: width="auto" height="auto" }
![vbox24.png](/assets/vbox24.png){: width="auto" height="auto" }
![vbox25.png](/assets/vbox25.png){: width="auto" height="auto" }

</details>


The next 3 steps will be very similar. refer to images if need be.

Select `Adapter 2`. Tick the *Enable Network Adapter option*. For the Attached to option select `Internal Network`. For Name enter `LAN 0`. Expand the Advanced section. For Adapter Type select `Paravirtualized Network (virtio-net)`.

Select `Adapter 3`. Tick the *Enable Network Adapter option*. For the Attached to option select `Internal Network`. For Name enter `LAN 1`. Expand the Advanced section. For Adapter Type select `Paravirtualized Network (virtio-net)`.

Select `Adapter 4`. Tick the Enable Network Adapter option. For the Attached to option select `Internal Network`. For Name enter `LAN 2`. Expand the Advanced section. For Adapter Type select `Paravirtualized Network (virtio-net)`.

Once done click on `OK` to save the changes and close the configuration menu.

## VirtualBox Network Settings: All You Need to Know 

{: .warning }
VirtualBox by defualt only allows us to configure 4 interfaces using the UI. Towards the end of the guide we will see how to add more interfaces using VirtualBox Command line interface.

Additionally, you can find a [Virtualbox Network Settings Guide] here.

## pfSense Installation

Essentially, the installation process will be hitting quite a few times.

> To start select the pfSense VM from the sidebar and hit the `Start` icon.

*Please read along if you would like to confirm the correct setup steps.* 

> Initally, an agreement will appear. Press Enter if you would like to Accept the agreement. 

(note you will have to accept the agreement to use the features of this VM)

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox26.png](/assets/vbox26.png){: width="auto" height="auto" }
![vbox27.png](/assets/vbox27.png){: width="auto" height="auto" }
![vbox28.png](/assets/vbox28.png){: width="auto" height="auto" }
![vbox29.png](/assets/vbox29.png){: width="auto" height="auto" }
![vbox30.png](/assets/vbox30.png){: width="auto" height="auto" }
![vbox31.png](/assets/vbox31.png){: width="auto" height="auto" }
![vbox32.png](/assets/vbox32.png){: width="auto" height="auto" }
![vbox33.png](/assets/vbox33.png){: width="auto" height="auto" }
</details>

> Press Enter to start the Installation.

> Press Enter to select the Auto (ZFS) partition option.

> Press Enter to select Proceed with Installation.

> Press Enter to select Stripe - No Redundancy.

> Use the Spacebar key to select the Hard Drive (ada0) then press Enter to continue.

> Use the Left Arrow to select YES and then press Enter to continue.

Wait for the installation to complete.

Press Enter to Reboot the VM.


## pfSense Configuration

Once pfSense reboots, the first priority is to configure the adapters we created in the VirtualBox settings.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox26.png](/assets/vbox26.png){: width="auto" height="auto" }
![vbox27.png](/assets/vbox27.png){: width="auto" height="auto" }
![vbox28.png](/assets/vbox28.png){: width="auto" height="auto" }
![vbox29.png](/assets/vbox29.png){: width="auto" height="auto" }
![vbox30.png](/assets/vbox30.png){: width="auto" height="auto" }
![vbox31.png](/assets/vbox31.png){: width="auto" height="auto" }
![vbox32.png](/assets/vbox32.png){: width="auto" height="auto" }
![vbox33.png](/assets/vbox33.png){: width="auto" height="auto" }
</details>


> Should VLANs be set up now? n

> In the next step, we will configure the interfaces manually.


Enter the WAN interface name: `vtnet0`

Enter the LAN interface name: `vtnet1`

Enter the Optional 1 interface name: `vtnet2`

Enter the Optional 2 interface name: `vtnet3`

Do you want to proceed?: `y`

Since the `WAN` interface of pfSense is managed by VirtualBox, it has been assigned an IPv4 address by the VirtualBox DHCP server. pfSense has also assigned an IPv4 address to the `LAN` interface using its own DHCP service. The `OPT1` and `OPT2` interfaces have not been assigned any IP address yet.. We do not want the IP addresses of the interfaces to change on boot. 

We will have to assign static IPv4 addresses to the `LAN`, `OPT1` and `OPT2` interfaces.

{: .warning }
The IP address of the `WAN` interface can be different in your case since it is assignment randomly by the VirtualBox DHCP server.

## Configuring LAN (vtnet1)

> Enter `2` to select “Set interface(s) IP address”. 

Then again, 

> Enter `2` to select the LAN interface.

Configure IPv4 address LAN interface via DHCP?: `n`

Enter the new LAN IPv4 address: `10.0.0.1`

Enter the new LAN IPv4 subnet bit count: `24`

![vbox34.png](/assets/vbox34.png){: width="auto" height="auto" }

----

> For the next question just press `Enter` for none. 

Because this is a `LAN` interface, we will not have to worry about configuring the upstream gateway.


Configure IPv6 address LAN interface via DHCP6: `n`

For the new LAN IPv6 address question press `Enter`

Do you want to enable the DHCP server on LAN?: `y`

Enter the start address of the IPv4 client address range: `10.0.0.11`

Enter the end address of the IPv4 client address range: `10.0.0.243`

Do you want to revert to HTTP as the webConfigurator protocol?: `n`

![vbox35.png](/assets/vbox35.png){: width="auto" height="auto" }

----

pfSense will use the inputs we provided and automatically configure the interface.

> Press `Enter` to complete the `LAN` interface configuration.

![vbox36.png](/assets/vbox36.png){: width="auto" height="auto" }

## Configuring OPT1 (vtnet2)

Enter `2` to select “Set interface(s) IP address”. Enter `3` this time in order to select the `OPT1` interface.

Configure IPv4 address OPT1 interface via DHCP?: `n`

Enter the new OPT1 IPv4 address: `10.6.6.1`

Enter the new OPT1 IPv4 subnet bit count: `24`

![vbox37.png](/assets/vbox37.png){: width="auto" height="auto" }

----

> For the next question directly press `Enter`. 

Since `OPT1` is a `LAN` interface we do not have to worry about configuring the upstream gateway.

Configure IPv6 address OPT1 interface via DHCP6: `n`

For the new OPT1 IPv6 address question press `Enter`

Do you want to enable the DHCP server on OPT1?: `y`

Enter the start address of the IPv4 client address range: `10.6.6.11`

Enter the end address of the IPv4 client address range: `10.6.6.243`

Do you want to revert to HTTP as the webConfigurator protocol?: `n`

Press `Enter` to save the changes and return to the main menu.

## Configuring OPT2 (vtnet3)

Enter `2` to select “Set interface(s) IP address”. Enter `4` to select the `OPT2` interface.

Configure IPv4 address OPT2 interface via DHCP?: `n`

Enter the new OPT2 IPv4 address: `10.80.80.1`

Enter the new OPT2 IPv4 subnet bit count: `24`

![vbox38.png](/assets/vbox38.png){: width="auto" height="auto" }

----

> For the next question directly press `Enter`. 

Since `OPT2` is a `LAN` interface we do not have to worry about configuring the upstream gateway.


Configure IPv6 address OPT2 interface via DHCP6: `n`

For the new OPT2 IPv6 address question press `Enter`

Do you want to enable the DHCP server on OPT2?: `n`

{: .warning }
OPT2 will be used for the Active Directory (AD) Lab. The Domain Controller (DC) in the lab will act as the DHCP server. Since the DC will perform DHCP, this is why we have disabled DHCP IP address assignment for this interface in pfSense.

Do you want to revert to HTTP as the webConfigurator protocol?: `n`

![vbox39.png](/assets/vbox39.png){: width="auto" height="auto" }

## Final Checks!

Press `Enter` to save the changes and return to the main menu.

The IP addresses for the `LAN`, `OPT1` and `OPT2` interfaces should be as follows:

![vbox40.png](/assets/vbox40.png){: width="auto" height="auto" }

Once confirmed, we have completed the configuration of the interfaces for our pfSense. However, there are still some additional settings that need to be configured. We will change these settings once we set up Kali Linux in the next module. From Kali Linux, we will access the pfSense Web Interface and proceed from there.

{: .warning }
pfSense Web Interface can be accessible for all the `LAN` interfaces in our `LAN`!

## Shutdown pfSense

When we start the lab pfSense is the first VM that has to be booted. When we shut down the lab pfSense will be the ***last*** VM that is stopped.

> From the Main Menu

Enter the option: `6` (Halt system) 

Do you want to process?: `y`

This will initiate the shutdown sequence.

## Post-Installation Cleanup

After the VM is shut down. Click on Settings from the toolbar.

Go to the `Storage` tab. 
In the Storage Devices section click on the pfSense `.iso` image then click on the small disk image on the right side of the Optical Drive option.

From the dropdown select `Remove Disk` from `Virtual Drive`. Click on `OK` to save the changes and close the configuration menu.

The .iso file along with the .iso.gz file that was downloaded to create the VM can be deleted if you do not want to store them.

In the next module, we will set up `Kali Linux` on the `LAN` interface. This VM will be used to configure and manage pfSense. It will also be used as the attack VM to target the vulnerable systems on the `OPT1` (CYBER_RANGE).

Next part - Kali Linux Setup

[Download]: https://www.pfsense.org/download/
[Virtualbox Network Settings Guide]: https://www.nakivo.com/blog/virtualbox-network-setting-guide/