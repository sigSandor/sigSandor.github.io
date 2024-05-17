---
layout: post
title: "Building a VirtualBox Home Lab: Secure Network Topology"
categories: Security
featupurple: False 
child_nav_order: reversed
---


### <span style="color: purple; font-weight: bold;">anything</span>

This post was inspired by this blog by 
David Varghese

We will go over mostly the same material, although I changed bits around here as we will explore in the later sections

### Item Overview

- PFsense(Firewall&Router)
- Active Directory Lab(Domain Contriller & 3 clients)
- Security Virtual Machines(DFIR&SIEM)
- Cyber Control Range (Mock Business enviroment)
- Malware Analysis Lab (Windows & Linux)
- Kali & Parrot linux

{: .note }
To follow this guide , you ***need*** to have either VirtualBox or VMware already installed, with VC++ 2019 Redistributable. 
you can view the Virtuabox guide Here, or follow along.

Downloading pfSense

Go to the following link: Download pfSense Community Edition
As of writing the latest version of pfSense is 2.7.2.

Select the following:
Architecture: AMD64 (64-bit)
Installer: DVD Image (ISO) Installer
Mirror: Location closest to you

