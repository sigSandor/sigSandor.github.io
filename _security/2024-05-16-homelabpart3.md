---
layout: post
title: "Part 3 - Parrot Security (Linux setup)"
categories: Security
parent: Network & Security Home Lab
nav_order: 3
nav_exclude: false
---

{: .text-center }
# Network & Security Home Lab: 

![banner](/assets/banner.jpg){: width="auto" height="auto" }
###### Posted ***June 16, 2024***

{: .text-center }
## <span style="color: orange; font-weight: bold;">Part 3 - Parrot Linux setup</span>


In this module, we are going to install Parrot OS. This VM will be used for ethical hacking and management.

We will use this VM in the next module also to complete the pfSense final setup.

## <span style="color: royalblue; font-weight: bold;">Download Parrot Linux</span>

Go to the following link: `Download` > [Parrot linux] 

As of writing the latest version of Parrot is `6.1 Lorikeet`

![vbox41.png](/assets/vbox41.png){: width="auto" height="auto" }

- Download the recommended VirtualBox `.ova`. The image is around 7GB in size so it will take some time to download.

> Once it is downloaded we should have an `.ova` file.

- Move this file to the folder where the pfSense iso was also stored.

{: .warning}
Since this is a .ova file, you will `import` not Create `new`. In VirtualBox.

----

## <span style="color: royalblue; font-weight: bold;">ParrotSec VM Creation</span>

- Open VirtualBox. 

- Select `Machine` from the toolbar and then click on `Import`.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox42.png](/assets/vbox42.png){: width="auto" height="auto" }

</details>

- Select the folder where the Parrot `.ova` is stored, then hit `Next`

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox43.png](/assets/vbox43.png){: width="auto" height="auto" }

</details>


> For the Appliance Settings, select Generate new mac addresses, then hit `Next`. 

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox44.png](/assets/vbox44.png){: width="auto" height="auto" }

</details>

{: .warning }
You are able to change values later on for hardware resources if need be.

> Click on `Finish`.

> Lastly, there will be an Agreenment to Accept or Deny. Once accepted, the `.OVA` appliance will begin importing.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox45.png](/assets/vbox45.png){: width="auto" height="auto" }

</details>

----

## <span style="color: royalblue; font-weight: bold;">Adding VM to Group </span>

> Right-click on the Parrot VM from the sidebar, select Move to Group -> `New`.

> Right-click on the group name and select `Rename Group`. Name the group `Management`.

> Now we are going to create a nested group for our home lab.

Select the Firewall and Management group `(Ctrl+Click)`. Right-click on the name of one of the groups. From the menu select Move to Group -> [New].

Now both the groups should be nested inside the `New Group` . Right-click on the group and choose `Rename Group`. Give our group the name `Home Lab`.

Double check, now we should have the following structure:

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox46.png](/assets/vbox46.png){: width="auto" height="auto" }

</details>

----

# <span style="color: royalblue; font-weight: bold;">Parrot Updating</span>

- When Parrot boots, after a couple seconds it will ask to search for updates.

- Hit `Yes` to check for updates.

![vbox47.png](/assets/vbox47.png){: width="auto" height="auto" }

## <span style="color: royalblue; font-weight: bold;">Default password</span>

- It will ask for a root password.

{: .warning }
We need to change the default credentials, they are by default: 

```scss
user: parrot
password: parrot
```
<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox48.png](/assets/vbox48.png){: width="auto" height="auto" }

![vbox49.png](/assets/vbox49.png){: width="auto" height="auto" }

</details>

- Once updated, find the terminal on the top right of the machine.

> Run the following command: 

```scss
sudo apt autoremove
```

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

</details>

> Now run:

```scss
sudo shutdown now
```

----

## <span style="color: royalblue; font-weight: bold;">Network Configuration</span>

Go to `Network -> Adapter 1`. For the Attached to field select `Internal Network`. For Name select `LAN 0`. Expand the 
*Advanced* section. For *Adapter Type* select `Paravirtualized Network (virtio-net)`.

![vbox50.png](/assets/vbox50.png){: width="auto" height="auto" }


## <span style="color: royalblue; font-weight: bold;">Changing Default password/IP a</span>

> Select pfSense from the sidebar and click on `Start` on the toolbar.

> Select Parrot OS Security Edition from the sidebar and click on `Start` on the toolbar.

> Once Parrot starts, find the terminal in the top left.

-  We will run a series of commands, *firstly* to identify if pfSense issued an IP address in the correct subnet, and *secondly* to change the password.

{: .warning}
You should also change the default username.


```scss
ip a
```

![vbox51.png](/assets/vbox51.png){: width="auto" height="auto" }

- We can confirm the right subnet is designated by cross referencing the pfSense router. See below.

<details markdown="block">
<summary> <span style="color: orange; font-weight: bold;">Image Ref. (click me!)</span> </summary>

![vbox53.png](/assets/vbox53.png){: width="auto" height="auto" }

</details>


```scss
sudo su

passwd user
```

![vbox52.png](/assets/vbox52.png){: width="auto" height="auto" }


{: .warning }
If you often forget your passwords, you can stop at this point and create a new *clone* using VirualBox.

 
### <span style="color: royalblue; font-weight: bold;">Post-Installation Configuration (Optional)</span>

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


In the next module, we will access the pfSense Web UI and complete the remaining configuration.

### [Home Lab Part 4]({{site.baseurl}}/security/2024-05-16-homelabpart4/){: .btn .btn-green }




[Parrot linux]: https://parrotsec.org/download/