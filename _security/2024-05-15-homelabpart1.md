---
layout: post
title: "Network & Security Home Lab"
categories: Security
has_children: true
nav_order: 1
nav_exclude: false
---

{: .text-center }
# Network & Security Home Lab: 

### <span style="color: orange; font-weight: bold;">Part 1 - Introduction</span>

![banner](/assets/banner.png){: width="auto" height="auto" }

###### Posted ***May 20, 2024***
This guide was inspired by David Varghese's [blog] post.

The following guide will not be easy or short, it will be catering to entry level IT and CyberSecurity folk who already have a basic understanding of virtualbox, virtualization, and windows experience.

----

## Item Overview

- PFsense (Firewall&Router)
- Active Directory Lab( Domain Controller & 3 clients)
- Security Virtual Machines (DFIR&SIEM)
- Cyber Control Range (Mock Enterprise enviroment)
- Malware Analysis Lab (Windows & Linux)
- Kali & Parrot linux

## System Recommended Requirements
- Windows 7 or 10 host OS
- 64-bit multi-threaded CPU (minimum 4 cores) with Virtualization Support
- 16GB RAM
- 500gb - 1TB Disk Space

{: .warning }
You can check if Virtualization is enabled by pressing *Shift>Control>Esc* at the same time to open ***Task Manager***. There, under the Performance tab you can see if virtualization is enabled

![taskm1](/assets/taskm1.png)


To follow along successfully, you ***should*** have either [VirtualBox] or VMware already installed, with [VC++] 2019 Redistributable and as well as enable VBox guest additions. 

You can also view a [Virtualization Guide] on this page.


In the next module, we will start with the installation and configuration of pfSense.




[VirtualBox]: https://www.virtualbox.org/wiki/Downloads

[Virtualization Guide]: https://bce.berkeley.edu/enabling-virtualization-in-your-pc-bios.html

[VC++]: https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170

[blog]: https://blog.davidvarghese.dev/posts/building-home-lab-part-1/