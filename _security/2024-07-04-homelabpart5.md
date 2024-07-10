---
layout: post
title: "Part 5 - Cyber Range setup"
categories: Security
parent: Network & Security Home Lab
nav_order: 5
nav_exclude: false
---

{: .text-center }
## Network & Security Home Lab: 

![banner](/assets/banner.jpg){: width="auto" height="auto" }
###### in progress ***June 24, 2024***

{: .text-center }
### <span style="color: orange; font-weight: bold;">Part 5 - Cyber Range setup</span>




## <span style="color: royalblue; font-weight: bold;">VM 1: Metasploitable 2</span>

> For the Metasploitable 2 download,

Go to: [Metasploitable: 2 ~ VulnHub]

You will have to open the `.ZIP` and look for the `.vmdk` to extract.
It will be the largest file in the folder, and you should extract it to the same directory of your choosing.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox101](/assets/vbox101.png)

</details>

### <span style="color: royalblue; font-weight: bold;">Creating the Metasploitable 2.0 VM</span>

- Launch VirtualBox. Then click on `New` from the toolbar.


- Input the name as "Metasploitable 2.0", and make sure that the Folder location is set where the rest of the VMs for the Home Lab are going to be saved. 

*Leave the ISO Image option empty.*

- Select the `Linux Debian (64 bit)` as shown below and then click on `Next`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox102](/assets/vbox102.png)

</details>


On the next page,
- Reduce the Memory to 1024MB and click on `Next`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox103](/assets/vbox103.png)

</details>

Next,
Select ***“Do Not Add a Virtual Hard Disk”*** and click on `Next`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox104](/assets/vbox104.png)

</details>

The `.vmdk` file we downloaded is the Hard Disk, so no need to create one.
All we have to do is attach it.


- Confirm that everything looks correct and click on `Finish`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox105](/assets/vbox105.png)

</details>

- You will get a Warning as shown in the below image. Ignore it and click on `Continue`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox106](/assets/vbox106.png)

</details>


### <span style="color: royalblue; font-weight: bold;">Adding VM to Group</span>

> Right-click on the Metasploitable VM. Select Move to Group -> [New].

> Right-click on the group that is created and select Rename Group. Call the group Cyber Range.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox107](/assets/vbox107.png)

</details>

- The output should look as follows:

![vbox108](/assets/vbox108.png)

> Right-click on the Cyber Range group and select Move to Group -> Home Lab.

- The final output should look as follows:

![vbox109](/assets/vbox109.png)

### <span style="color: royalblue; font-weight: bold;">Configuring the VM</span>

> Select the Metasploitable 2.0 from the sidebar and then from the toolbar click on `Settings`.

> Go to Storage and select Controller: SATA then click on the small “Add Hard Disk” icon on the right.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox110](/assets/vbox110.png)

</details>

This will open the Hard Disk Selector menu. 

> Click on `Add` and then select the `.vmdk` file. Then click on the `Open` button to use the Hard Drive.

If done correctly under Controller: SATA the Hard Disk will be visible.

![vbox111](/assets/vbox111.png)

> Go to System -> Motherboard. For Boot Order ensure that the Hard Disk is on the *top* followed by Optical. *Disable Floppy*.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox112](/assets/vbox112.png)

</details>

Go to `Network` -> `Adapter 1`. Change the Attacked to field to `Internal Network` and in Name select `LAN 1`. Click on `OK` to save the changes.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox113](/assets/vbox113.png)

</details>

### <span style="color: royalblue; font-weight: bold;">Testing Connectivity</span>

From the sidebar select Metasploitable 2 and then click on Start.

Once the VM boots use the following credentials to log in.

````scss
Username: msfadmin
Password: msfadmin
````
<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox114](/assets/vbox114.png)

</details>

After login use the following command to check if we have an IP address:

````scss
ip a l eth0
````

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox115](/assets/vbox115.png)

</details>

![vbox118](/assets/vbox118.png)

- We can see that we have been assigned the IP 10.6.6.11 (IP may be different) which we know is inside the DHCP address range for the CYBER_RANGE interface.

We can ping Google to test if we have an Internet connection.

````scss
ping google.com -c 5
````

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox116](/assets/vbox116.png)

</details>

### <span style="color: royalblue; font-weight: bold;">Pinging Metasploitable 2.0 -> Parrot</span>




## <span style="color: royalblue; font-weight: bold;">VM 2: Chronos</span>

> For the Chronos download

Go to : [Chronos: 1 ~ VulnHub]

The downloaded file will be another `.ova` file.

> Move the .ova to the same directory we were using before.

![vbox119](/assets/vbox119.png)

### <span style="color: royalblue; font-weight: bold;">Creating the VM</span>

> From the VirtualBox sidebar select the Cyber Range group, then `File` -> `Import`.

![vbox120](/assets/vbox120.png)

> From the Import screen select the icon, select the .ova and hit `Next`.

![vbox121](/assets/vbox121.png)

From the next menu, we can change some of the configuration. You can change the name as you like. For `MAC Address Policy` ensure that *Generate new MAC addresses for all network adapters is selected*. If everything looks right click on `Finish`.

![vbox122](/assets/vbox122.png)

{: .warning}
Importing can take a little while.


### <span style="color: royalblue; font-weight: bold;">Adding VM to Group</span>

>Once the import is finished, right-click on the VM and then select `Move to Group` -> `Home Lab/Cyber Range`.

or

> Drag it into the Cyber range group

The result result will be as follows: 

![vbox123](/assets/vbox123.png)


### <span style="color: royalblue; font-weight: bold;">Configuring the VM</span>

Select the Chronos VM, then `Settings`.

Go to `System` -> `Motherboard`. For Boot Order ensure that `Hard Disk` is on the top followed by `Optical`. `Disable Floppy`.

![vbox124](/assets/vbox124.png)

Go to `Network` -> `Adapter 1`. For the Attached to field select `Internal Network`, for name select `LAN 1`. Expand the Advanced settings option. From Adapter Type select `Paravirtualized Network (virtio-net)`. Click `OK` to save the changes.

![vbox125](/assets/vbox125.png)

### <span style="color: royalblue; font-weight: bold;">Testing Connectivity</span>

Select the Chronos VM and from the toolbar select `Start`. Once the VM starts we should see the login screen. The credentials for this machine are not known so we cannot log in and check if it has been assigned an IP address.

On the Kali Linux VM open the pfSense Web Portal. From the navigation bar select Status -> DHCP Leases.

![vbox126](/assets/vbox126.png)

Under the Leases section, there should be an entry for Chronos. We can see that it has been assigned the IP 10.6.6.12.

{: .warning}
Adapter Type Selection
You would have noticed that for the Metasploitable 2 VM we did not chose Paravirtualized Network. This VM is quite old and does not work properly on that Adapter. Windows VMs also don’t work on Paravirtualized Network Adapter.
From a performance point of view Paravirtualized Network is the better choice. We don’t have a way to know in advance if a Linux VM will work on the Adapter. So what I recommend is to first select Paravirtualized Network booting up the VM and check if the network is working properly if not shutdown the VM and select a different Adapter.

In the next module, we will begin configuring the Active Directory Lab.

### [Home Lab Part 6]({{site.baseurl}}/security/2024-07-04-homelabpart6/){: .btn .btn-green }


[Chronos: 1 ~ VulnHub]: https://www.vulnhub.com/entry/chronos-1,735/
[Metasploitable: 2 ~ VulnHub]: https://www.vulnhub.com/entry/metasploitable-2,29

