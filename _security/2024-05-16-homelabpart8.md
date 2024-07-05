---
layout: post
title: "Building a VirtualBox Home Lab: Secure Network Topology Part 1"
categories: Security
parent: Network & Security Home Lab
nav_order: 8
nav_exclude: true
---


## Network & Security Home Lab: 

### <span style="color: pink; font-weight: bold;">Part 1 - Secure Network Topology</span>

![banner](/assets/banner.jpg){: width="auto" height="auto" }

###### Posted ***May 15, 2024***

Building a Virtual Security Home Lab: Part 8 - Malware Analysis Lab Setup




In the module, we are going to set up the Malware Analysis Lab. This lab will consist of two VMs. One of the VMs will be for Windows Malware Analysis and the other one will be for Linux Malware Analysis.

## <span style="color: royalblue; font-weight: bold;">Creating New Interface</span>

VirtualBox GUI does not allow us to create more than four Network Interfaces.

However, we can configure up to 8 interfaces per VM. To add more than 4 interfaces we have to utilize the VirtualBox CLI.

## <span style="color: royalblue; font-weight: bold;">VirtualBox CLI Setup</span>

The VirtualBox CLI binary is called VBoxManage.exe.

To be able to use the CLI we have to add its path as an environment variable.
VirtualBox is by default installed at C:\Program Files\Oracle\VirtualBox.

Copy the path to the executable from the navigation bar.

Open Search and type “Environment”. Click on Edit environment variables for your account.

In the top window select the variable named “Path” and then click on Edit.

Click on New and then paste the path to the VirtualBox CLI. Then click on OK.

Click on OK to close the Environment Variables menu.

To test if the variable was added successfully open PowerShell and run the following command:

# List all installed VMs
VBoxManage list vms

Creating new Interface

Before we create the new interfaces we need to know the name of the pfSense VM (it is “pfSense” in my case). The VM should also be “Powered Off”.

To add a network interface run the following commands:

# Create a Internet Network
VBoxManage modifyvm "pfSense" --nic5 intnet

# Use the Paravirtualized Adapter
VBoxManage modifyvm "pfSense" --nictype5 virtio

# Give it the name LAN 3
VBoxManage modifyvm "pfSense" --intnet5 "LAN 3"

# Network Interface is connected by Cable
VBoxManage modifyvm "pfSense" --cableconnected5 on

    In the above commands “pfSense” is the name of my VM.
    In the 3rd command in place of “LAN 3” you can use a different name that matches your network interface naming convention.

Now if we look at the overview of the pfSense VM we should see Adapter 5.

    Interfaces that are created using the CLI will not show up in the Settings page for the VM. If you want to modify the adapter settings you have to do it using the CLI.

###  <span style="color: royalblue; font-weight: bold;">Enabling the Interface</span>

Start the pfSense VM. On boot, you will notice that there are still only 4 interfaces. The new interface has to be onboarded before it shows up in pfSense.

Enter 1 to select “Assign Interfaces”.
Should VLANs be set up now? n

Enter the WAN interface name: vtnet0
Enter the LAN interface name: vtnet1
Enter the Optional 1 interface name: vtnet2
Enter the Optional 2 interface name: vtnet3
Enter the Optional 3 interface name: vtnet4

Do you want to proceed?: y

The new interface has been added. Now we need to assign the interface an IP address.

Enter 2 to select “Set interface(s) IP address”
Enter 5 to select the OPT3 interface.

Configure IPv4 address OPT3 interface via DHCP?: n
Enter the new OPT3 IPv4 address: 10.99.99.1
Enter the new OPT3 IPv4 subnet bit count: 24

For the next question press Enter. Since we are configuring a LAN interface we do not have to worry about the upstream gateway.

Configure IPv6 address OPT3 interface via DHCP6: n
For the new OPT3 IPv6 address question press Enter.
Do you want to enable the DHCP server on OPT3?: y
Enter the start address of the IPv4 client address range: 10.99.99.11
Enter the end address of the IPv4 client address range: 10.99.99.243
Do you want to revert to HTTP as the webConfigurator protocol?: n

Now interface OPT3 will have an IP address.

### <span style="color: royalblue; font-weight: bold;">Renaming the Interface</span>

Launch the Kali Linux VM. Login to the pfSense web portal. From the navigation bar select Interfaces -> OPT3.

In the description field enter ISOLATED. Scroll to the bottom and click on Save.

Click on Apply Changes in the popup that appears to persist the changes.

### <span style="color: royalblue; font-weight: bold;">Interface Firewall Configuration</span>

From the navigation bar click on Firewall -> Rules.

Select the ISOLATED tab. Click on the “Add” button to create a new rule.

Change the values as follows:
Action: Block
Address Family: IPv4+IPv6
Protocol: Any
Source: ISOLATED subnets
Description: Block access to everything

Scroll to the bottom and click on Save.

In the popup click on Apply Changes to persist the new rule.

    Since this Interface is going to be used for Malware Analysis we are blocking network access. This will ensure that malware cannot spread to other systems using the network.

### <span style="color: royalblue; font-weight: bold;">Reboot pfSense</span>

Now we need to restart pfSense to ensure that the firewall rules are propagated properly. From the navigation bar select Diagnostics -> Reboot.

Click on Submit.

Once pfSense boots up you will be redirected to the login page.

## <span style="color: royalblue; font-weight: bold;">Flare VM Setup</span>

To install Flare we need a Windows machine. Flare can be set up using most versions of Windows. Since we already have the ISO for Windows 10 Enterprise I will be using it to configure Flare.

### <span style="color: royalblue; font-weight: bold;">Windows ISO Download</span>

Go to the following URL: Windows 10 Enterprise | Microsoft Evaluation Center

Click on the 64-bit edition Enterprise ISO download option. The ISO file is ~5GB.

### Creating the VM

Select Tools from the sidebar and click on New.

Give the VM a name. Select the downloaded Windows 10 ISO Image. Check “Skip Unattended Installation”. Then click on Next.

Increase Base Memory to 4096MB and click on Next.

Increase the Drive Size to 100GB and click on Next.

Verify all the settings and click on Finish.

Adding VM to Group

Right-click on the VM and select Move to Group -> [New].

Right-click on the group and rename it to “Malware Analysis”.

Right-click on the “Malware Analysis” group and select Move to Group -> Home Lab.

The final result should look as follows:

### <span style="color: royalblue; font-weight: bold;">Configuring the VM</span>

Select the VM then from the toolbar select Settings.

Go to System -> Motherboard. In the Boot Order field ensure that Hard Disk is on the top followed by Optical. Uncheck Floppy.

Leave the Network Adatper on its default setting of NAT.

    Machines assigned to the ISOLATED interface does not have internet connection. But to setup Flare we need Internet access. Once we finish the configuring Flare we will move it to the correct subnet.

Click on OK to save the settings.

### <span style="color: royalblue; font-weight: bold;">Installing Windows</span>

Select the Flare VM from the sidebar and click on Start.

Install Windows as shown below. The installation process is identical to the process from the previous module (Part 7).

Select “Domain join instead”.

    Provide a name that does not use special characters and spaces. This is very important. The installer for Flare will not work otherwise.

Once on the desktop Windows will ask should access to the Internet be allowed click on Yes.

### <span style="color: royalblue; font-weight: bold;">Guest Additions Installation</span>

Install Guest Additions to enable the resizing on the VM display. Once again you can refer to the last module (Part 7) for more detailed steps.

After rebooting the VM. Remove the Guest Addition Image.

### Creating VM Snapshot 1

Before we proceed we are going to take a snapshot of the VM. Snapshots allow us to roll back to an old functional state of the VM.

Shut down the VM. Click on the Hamburger menu on the right of the VM name in the sidebar. Select Snapshots.

Click on Take.

Give the Snapshot a descriptive name. Click on OK to create the Snapshot.

Click on the Hamburger menu and click on Details to return to the original page.

### Flare VM Pre-Install Configuration

You can read more about Flare VM and its pre-requisites on the below link:
mandiant/flare-vm: A collection of scripts to setup a reverse engineering environment

TLDR; “Windows Updates” and “Windows Defender” have to be disabled.

#### Disabling Windows Update

How to change account password on Windows 11 | Windows Central

Open on Search bar and search for “Settings”. Open the Settings app.

Click on “Update & Security”.

Click on the “Pause updates for 7 days” button.

#### Disabling Windows Defender

Download the following script: jeremybeaume/tools: Script to disable Windows Defender

Right-click on the Shield icon on the taskbar and select “View Security Dashboard”.

Click on “Virus & threat protection”.

Select “Manage settings” from the “Virus & threat protection settings” section.

Disable all the features that are shown in the image below:

Right-click on the Start menu and select “Windows PowerShell (Admin)”.

Run the following command to download the script:

# Save the script in the Downloads folder
Invoke-WebRequest "https://raw.githubusercontent.com/jeremybeaume/tools/master/disable-defender.ps1" -OutFile $HOME\Downloads\disable-defender.ps1

Use the shortcut Windows+R to open the Run dialog. Enter msconfig and click on OK.

Navigate to the Boot tab. In the Boot options section enable “Safe boot” and then click on OK to save changes.

Click on Restart to boot into Safe Mode.

In Safe Mode, the VM cannot be resizable. Safe Mode essentially disables all features that are not required to run the OS.

Right-click on the Start menu and select “Windows PowerShell (Admin)” and enter the following commands:

# Change directory
cd .\Downloads\
# Unblock the downloaded script
Unblock-File .\disable-defender.ps1
# Disable the PowerShell policy preventing script execution 
Set-ExecutionPolicy Unrestricted -Force
# Start the script
.\disable-defender.ps1

Once the script completes its execution press Enter to close the script. Reboot the VM for the changes to take place.

Press Windows+R to open the Run dialog. Enter msconfig and click on OK.

Navigate to the Boot tab. From the Boot options section disable “Safe boot”. Click on Apply then OK. Restart the VM to boot normally into Windows.

Wait for some time for Defender to load completely and then you will see that “Virus & threat protection” will show as disabled. This means that the script worked successfully.

### Renaming the VM

Search for “This PC” and from the right side click on “Properties”.

Select “Rename this PC”.

Give the PC a name. Click on Next and then select “Restart Now” for the changes to take effect.

### Creating VM Snapshot 2

Shut down the VM. Go to the Snapshot page using the Hamburger menu. Click on Take to create a new Snapshot.

Give the Snapshot a descriptive name. Then click on OK.

Use the Hamburger menu and return to the Details page. Click on Start to start the VM.

## <span style="color: royalblue; font-weight: bold;">Flare VM Installation</span>

Right-click on the Start menu and select “Windows PowerShell (Admin)”.

Enter the following commands to download and run the Flare VM script.

# Download the FlareVM script
Invoke-WebRequest "https://raw.githubusercontent.com/mandiant/flare-vm/main/install.ps1" -OutFile $HOME/Downloads/install.ps1
# Go to Downloads Folder
cd $HOME/Downloads
# Unlock the downlaoded script
Unblock-File .\install.ps1
# Disable PowerShell script execution policy 
Set-ExecutionPolicy Unrestricted -Force
# Run the script
.\install.ps1

The script will make some checks before starting the installation.

Enter Y when asked about Snapshot. Enter password when prompted.

After some time the Flare VM configuration dialog will open.

In the Package Installation Customization section from the left side select “debloat.vm” and click on the right arrow to select it for installation.

Click on OK to start the install. The VM will restart multiple times during the setup.

The installation can take a very long time. Once the setup is complete we will get the following prompt click on Finish to complete the setup.

After the installation is complete. Restart the VM to complete the setup.

## <span style="color: royalblue; font-weight: bold;">Post-Install Configuration</span>

### Installing OpenSSH Server

Once we move this VM to the ISOLATED subnet it will not be able to access the internet. We will not be able to download malware samples directly from the Internet. We will download the samples onto a different VM that has Internet access and then move them to this machine using SSH. I will cover this process in more detail in a later module. For now, we need to install “OpenSSH Server”.

Open the Search bar. Type “Add” and from the results select the “Add or remove programs” option.

Click on Optional Features under “Apps & features”.

Click on Add a feature. This will open a new menu.

Search for “SSH”. Enable “OpenSSH Server” and then click on Install.

Once the install is complete if you search for “SSH” in the “Installed features” section you should see “OpenSSH Client” and “OpenSSH Server”.

## <span style="color: royalblue; font-weight: bold;">Moving VM to the Isolated Network</span>

Shut down the VM. Open the VM Settings page and go to Network. For the Attached to field select Internal Network. For name select LAN 3. Click on OK to save the changes.

### Creating VM Snapshot 3

Using the Hamburger menu open the Snapshot page. Click on Take to create a Snapshot. Give the Snapshot a descriptive name and then click on Ok.

You can now delete the Windows 10 Enterprise ISO if you do not plan to store it in the future.

## <span style="color: royalblue; font-weight: bold;">REMnux VM Setup</span>

### Download Image

Go to the following link: Get the Virtual Appliance - REMnux Documentation

Click on Box to open the download page.

Click on the blue Download button. The image is ~5GB.

Once the download is complete we will have an .ova file.

### Creating the VM

Click on Tools from the sidebar and then select Import.

Select the downloaded OVA file and click on Next.

Configure the VM as required. Ensure the VM has 4096MB of RAM. For the MAC Address Policy select “Generate new MAC addresses for all network adapters” then click on Finish.

### Adding VM to Group

Once the import is complete right-click on the VM and select Move to Group -> Home Lab/Malware Analysis.

### Configuring the VM

Select the VM then click on Settings from the toolbar.

Go to System -> Motherboard. In Boot Order ensure that Hard Disk is on the top followed by Optical. Uncheck Floppy. Click on OK to save the changes.

### Post-Install Configuration

Select the VM and from the toolbar click on Start.

### Updating Guest Additions

The VM will already have Guest Additions installed but it will be an older version. From the VM toolbar select Devices -> Upgrade Guest Additions to update Guest Additions.

### Upgrading Packages

Once Guest Additions is updated open a Terminal and enter the following command to update the system packages.

remnux upgrade

Once the update is complete restart the VM.

## <span style="color: royalblue; font-weight: bold;">Moving VM to the Isolated Network</span>

Shut down the VM. Open the Settings menu and select Network.

For the Attached to option select Internal Network. For the name field select LAN 3. Click on OK to save the changes. This will move the VM to the ISOLATED interface that does not have internet access.

### Creating VM Snapshot

Click on the Hamburger menu and select Snapshot.

Click on Take to create a Snapshot.

Give the Snapshot a descriptive name. Then click on OK.

Use the Hamburger menu to go back to the Details page.

In the next, module we will start configuring the Security subnet. This subnet will have our DFIR VM and SIEM (Splunk).

<span style="color: royalblue; font-weight: bold;">Part 9 - Tsurugi Linux (DFIR) Setup</span>