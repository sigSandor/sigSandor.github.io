---
layout: post
title: "Part 4 - pfSense Firewall configuration"
categories: Security
parent: Network & Security Home Lab
nav_order: 4
nav_exclude: false

---

## Network & Security Home Lab: 

### <span style="color: pink; font-weight: bold;">Part 4 - pfSense Firewall configuration</span>

![banner](/assets/banner.png){: width="auto" height="auto" }

###### In Progress ***May 26, 2024***

Building a Virtual Security Home Lab: Part 3 - Kali Linux Setup

A step-by-step guide for building your very own Cybersecurity Home Lab using VirtualBox
Posted Jan 4, 2024
Preview Image
By David Varghese
5 min read

Banner Background by logturnal on Freepik
Hacker Image by catalyststuff on Freepik

In this module, we are going to install Kali Linux. We will use this VM in the next module also to complete the pfSense setup.
Download Kali Linux

Go to the following link: Get Kali | Kali Linux

Download the 64-bit Recommended Installer. The image is ~4GB in size so it will take some time to download.

As of writing the latest version of Kali Linux is 2023.4.

Once it is downloaded we should have an .iso file.

Kali Linux VM Creation

Launch VirtualBox. Select Tools from the sidebar and then click on New from the toolbar.

Give the VM a Name. Set the Folder option to the location where the Home Lab VMs are going to be saved. Leave the ISO Image option empty. Select Type as Linux and Version as Debian (64-bit) then click on Next.

Leave everything on its default values. Click on Next.

Increase the Disk Size to 80GB and click on Next.

Ensure that all the settings look right and click on Finish.

Adding VM to Group

Right-click on the Kali Linux VM from the sidebar, select Move to Group -> [New].

The VM will now be added to a Group called New Group. Right-click on the group name and select Rename Group. Name the group Management.

Select the Firewall and Management group (Ctrl+Click). Right-click on the name of one of the groups. From the menu select Move to Group -> [New].

Now both the groups should be nested inside a group called New Group. Right-click on the group and choose Rename Group. Give the group the name Home Lab.

In the end, we should have the following structure:

Kali Linux VM Configuration

Select the Kali Linux VM and then from the toolbar select Settings.

System Configuration

Go to System -> Motherboard. For the Boot Order option ensure that the Hard Disk is on the top followed by Optical. Uncheck Floppy.

Boot Image Configuration

Go to the Storage tab. Select the Empty disk present below Controller: IDE then click on the small disk icon on the right side of the Optical Drive option.

Select Choose a disk file and then select the downloaded .iso file for Kali Linux.

The final result should look as follows:

Network Configuration

Go to Network -> Adapter 1. For the Attached to field select Internal Network. For Name select LAN 0. Expand the Advanced section. For Adapter Type select Paravirtualized Network (virtio-net).

Kali Linux Installation

Remember to boot the pfSense VM if it was shut down before starting the Kali Linux installation.

Select Kali Linux from the sidebar and click on Start on the toolbar.

From the Installer menu select Graphical Install.

Select your Language, location and keyboard layout.

Enter a name for the VM. You can use any name here. The hostname is used to identify the system on the network. The hostname can also be changed after installation.

Leave the domain name input blank and click on Continue.

Enter your name. This name will be shown on the login screen.

The username is used to create the home directory for the user. All the user-related configurations are stored in this folder.

Enter a strong password. Re-enter the password in the second field and click on Continue.

Select your clock and then click on Continue.

Select the drive (sda) and click on Continue.

Select Guided - use entire disk and then click on Continue.

Select the option: All files in one partition and click on Continue.

Select Finish partitioning and write changes to disk. Then click on Continue.

Select Yes and click on Continue.

After the base system installation is complete we need to choose the desktop environment that will be installed. I have selected GNOME for installation.

The default is XFCE it does not look as pretty as GNOME it is much lighter and should have better performance. KDE Plasma is the fanciest with a lot of bells and whistles. I would only recommend KDE if you can assign 2 cores and 4GB RAM for this VM. Once the desktop environment is selected click on Continue.

The installation will take some time. Select Yes and click on Continue.

Click on Continue to Reboot the system.

After reboot, we should see the Login screen. Click Enter to log in. Enter the password that was configured during the installation.

Post-Installation Configuration

Kali Linux installer can detect when it is run from a VM because of this it automatically installs Guest Addons.

Press Right Ctrl+F to enter Fullscreen mode. The VM should scale to fill the entire screen. Press Right Ctrl+F again to exit Fullscreen mode. From the dock at the bottom of the screen. Select the Terminal.

Run the command: ip a. We can see that the Kali VM has been assigned an IP address from the LAN network range. The VM should be able to access the internet as well.

Use the following command to update the system:

sudo apt update && sudo apt full-upgrade

Enter password when prompted.

Once the sources have been fetched we will be asked if we want to continue. Enter Y and then press Enter to start the update.

After the update is complete run the following command to remove the unused packages:

sudo apt autoremove

The .iso file that was downloaded to create the VM can be deleted now if you do not plan to store it for future use.

In the next module, we will access the pfSense Web UI and complete the remaining configuration.