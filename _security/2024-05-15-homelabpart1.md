---
layout: post
title: "Network & Security Home Lab"
categories: Security
has_children: true
nav_order: 1
---

{: .text-center }
# Network & Security Home Lab: 

![banner](/assets/banner.jpg){: width="auto" height="auto" }
###### Posted ***May 20, 2024***

{: .text-center }
## <span style="color: orange; font-weight: bold;">Part 1 - Introduction</span>


{: .warning }
This series was inspired and follows a similar structure to David Varghese's [blog] guide.
However, I did my best to put my own spin on the home lab guide. 


----

## <span style="color: royalblue; font-weight: bold;">Item Overview</span>

- PFsense (Firewall & Router)
- Parrot linux
- Cyber Control Range 
- Malware Analysis Lab (Windows & Linux)
- Security Virtual Machines (DFIR & SIEM)
- Active Directory Lab



##  <span style="color: royalblue; font-weight: bold;">Recommended Requirements</span> 
- Windows 7 or 10 host OS (standalone from home and business os)
- 64-bit multi-threaded CPU (minimum 4 cores) with Virtualization Support enabled
- 16GB RAM
- 500gb - 1TB Free disk space


{: .warning }
You should check if virtualization is enabled right now, by pressing *Shift>Control>Esc* to open ***Task Manager***. Under the Performance tab you can see if virtualization is enabled

![taskm](/assets/taskm.png)


You should also already have [VC++] 2019 Redistributable installed as well.

You can view a [Virtualization Guide] on this page.


In the next module, we will start with the installation and configuration of pfSense.


### [Home Lab Part 2]({{site.baseurl}}/security/2024-05-16-homelabpart2/){: .btn .btn-green }

[VirtualBox]: https://www.virtualbox.org/wiki/Downloads

[Virtualization Guide]: https://bce.berkeley.edu/enabling-virtualization-in-your-pc-bios.html

[VC++]: https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170

[blog]: https://blog.davidvarghese.dev/posts/building-home-lab-part-1/

