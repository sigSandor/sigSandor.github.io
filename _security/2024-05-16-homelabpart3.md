---
layout: post
title: "Part 3 - Kali Linux setup"
categories: Security
parent: Network & Security Home Lab
nav_order: 3
nav_exclude: false
---

{: .text-center }
# Network & Security Home Lab: 

{: .text-center }
## <span style="color: orange; font-weight: bold;">Part 3 - Kali Linux setup</span>

![banner](/assets/banner.png){: width="auto" height="auto" }

###### Posted ***May 26, 2024***


In this module, we are going to install Kali Linux. This VM will be used for red teaming.

We will use this VM in the next module also to complete the pfSense final setup.

## Download Kali Linux

Go to the following link: `Download` > [Kali linux] 

As of writing the latest version of Kali Linux is `2024.2`

![vbox41.png](/assets/vbox41.png){: width="auto" height="auto" }

Download the 64-bit Recommended Installer. The image is around 4GB in size so it will take some time to download.

Once it is downloaded we should have an `.iso` file.
Move this file to the folder where the pfSense iso was also stored.

## Kali Linux VM Creation

> Open VirtualBox. 

> Select `Machine` from the toolbar and then click on `New`.

Name the VM, Kali linux. Set the Folder option to the location where the Home Lab VMs are going to be saved. 

***Leave the ISO Image option empty***

Select Type as `Linux` and Version as ` Debian (64-bit)` then click on `Next`.

![vbox42.png](/assets/vbox42.png){: width="auto" height="auto" }


> For the Hardware section, 2048 memory and 2 cores is enough (default values). 

![vbox43.png](/assets/vbox43.png){: width="auto" height="auto" }

{: .warning }
You are able to change values later on for hardware resources if need be.

>Click on `Next`.

Increase the Disk Size to `80GB` and click on `Next`.

![vbox44.png](/assets/vbox44.png){: width="auto" height="auto" }

Ensure that all the settings look right and click on Finish.

![vbox45.png](/assets/vbox45.png){: width="auto" height="auto" }

## Adding VM to Group

> Right-click on the Kali Linux VM from the sidebar, select Move to Group -> `New`.

> Right-click on the group name and select `Rename Group`. Name the group `Management`.

> Now we are going to creat a nested group for our home lab.

Select the Firewall and Management group `(Ctrl+Click)`. Right-click on the name of one of the groups. From the menu select Move to Group -> [New].

Now both the groups should be nested inside the `New Group` . Right-click on the group and choose `Rename Group`. Give our group the name `Home Lab`.

Double check, now we should have the following structure:

![vbox46.png](/assets/vbox46.png){: width="auto" height="auto" }

# Kali Linux VM Configuration

Select the Kali Linux VM and then from the toolbar select Settings.

## System Configuration

Go to `System` -> `Motherboard`. For the Boot Order option ensure that the `Hard Disk` is on the top followed by `Optical`. 

> `Uncheck Floppy`.

![vbox47.png](/assets/vbox47.png){: width="auto" height="auto" }

## Boot Image Configuration

> Go to the `Storage` tab.
Select the Empty disk present below `Controller: IDE` then click on the small disk icon on the right side of the Optical Drive option.

Select `Choose a disk file` and then select the downloaded `.iso` file we have for Kali Linux.


![vbox48.png](/assets/vbox48.png){: width="auto" height="auto" }

The final result should look as follows:

![vbox49.png](/assets/vbox49.png){: width="auto" height="auto" }

## Network Configuration

Go to `Network -> Adapter 1`. For the Attached to field select `Internal Network`. For Name select `LAN 0`. Expand the 
*Advanced* section. For *Adapter Type* select `Paravirtualized Network (virtio-net)`.

![vbox50.png](/assets/vbox50.png){: width="auto" height="auto" }


## Kali Linux Installation

***Remember to boot the pfSense VM first, before starting the Kali Linux installation.***

Select Kali Linux from the sidebar and click on `Start` on the toolbar.

> From the Installer menu select Graphical Install.

![vbox51.png](/assets/vbox51.png){: width="auto" height="auto" }

> The next steps will ask about your preffered Language, location and keyboard layout. 
select whatever makes sense for you, or just enter for default.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox52.png](/assets/vbox52.png){: width="auto" height="auto" }
![vbox53.png](/assets/vbox53.png){: width="auto" height="auto" }
![vbox54.png](/assets/vbox54.png){: width="auto" height="auto" }

</details>


On the next page, you will be required to enter a name for the VM. I simply put kali. 

The hostname is used to identify the system on the network. 

{: .warning }
The hostname can be changed after installation.

![vbox55.png](/assets/vbox55.png){: width="auto" height="auto" }

Leave the domain name input blank in the next section and click on *Continue*.

![vbox56.png](/assets/vbox56.png){: width="auto" height="auto" }

Next,
Enter your desired name and credentials. This name will be shown on the login screen.

![vbox57.png](/assets/vbox57.png){: width="auto" height="auto" }

{: .warning }
If you often forget your passwords, you can stop the installation at this point and create a new *clone* using VirualBox.

 
You can do so by right clicking on your (closed) VM and clicking clone. Or alternatively CNTL + O

### Username and Password

The username is used to create the home directory for the user. All the user-related configurations are stored in this folder.

![vbox58.png](/assets/vbox58.png){: width="auto" height="auto" }

Enter a strong password. Re-enter the password in the second field and click on Continue.

![vbox59.png](/assets/vbox59.png){: width="auto" height="auto" }

# Final steps

Select your `clock` and then click on `Continue` (Default is Central or Eastern).

Select the drive `(sda)` and click on `Continue` (Should be the only option).

Select *Guided - use entire disk* and then click on `Continue` (Easiest option, LVM is for advanced users).

Select the option: *All files in one partition* and click on `Continue`.

Select Finish partitioning and write changes to disk. Then click on `Continue`.

Select `Yes` to write changes to the disk, then click on `Continue`.

> Kali will begin installing the base system. 

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox60.png](/assets/vbox60.png){: width="auto" height="auto" }
![vbox61.png](/assets/vbox61.png){: width="auto" height="auto" }
![vbox62.png](/assets/vbox62.png){: width="auto" height="auto" }
![vbox63.png](/assets/vbox63.png){: width="auto" height="auto" }
![vbox64.png](/assets/vbox64.png){: width="auto" height="auto" }
![vbox65.png](/assets/vbox65.png){: width="auto" height="auto" }
![vbox66.png](/assets/vbox66.png){: width="auto" height="auto" }

</details>


## Desktop Enviroment

After the base system installation completes, we ahve to choose the desktop environment that will be installed. I have selected GNOME for installation. David Varghese also suggests this choice, as KDE is a bit more resource heavy and XFCE is default. You can make a personal choice here, but I like GNOME desktop enviroment.

> You will also be asked to confirm the installation of the GRUB boot loader which is necessary.

![vbox67.png](/assets/vbox67.png){: width="auto" height="auto" }
![vbox68.png](/assets/vbox68.png){: width="auto" height="auto" }
![vbox69.png](/assets/vbox69.png){: width="auto" height="auto" }

----

The installation will take some time. 

> The final question will just ask about rebooting.

![vbox70.png](/assets/vbox70.png){: width="auto" height="auto" }

Click on `Continue` to Reboot the system.

After reboot, we should see the Login screen. Once you enter your created password, Click `Enter` to log in. 

###   Post-Installation Configuration

Kali Linux installer can detect when it is run from a VM because of this it automatically installs Guest Addons.

> Select the Terminal.

Run the command: `ip a`. We can see what the Kali VM has been assigned for an IP address from the LAN network range. The VM should be able to access the internet now.

> Use the following command in the terminal to update the system:

```scss
sudo apt update && sudo apt full-upgrade
```

Enter password when prompted.

Once the sources have been fetched we will be asked if we want to continue. Enter `Y` and then press Enter to start the update.

After the update is complete run the following command to remove the unused packages:

```scss
sudo apt autoremove
```

The `.iso` file that was downloaded to create the VM can be deleted now if you do not plan to store it for future use.

In the next module, we will access the pfSense Web UI and complete the remaining configuration.

Part 4 - pfSense Firewall Configuration



[Kali linux]: https://www.kali.org/get-kali/#kali-installer-images