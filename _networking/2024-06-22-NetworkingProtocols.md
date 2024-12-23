---
layout: post
title: "Networking 101" 
categories: Networking
has_children: true
nav_order: 1
nav_exclude: false
---

{: .text-center }
# Networking 101

![netw1](/assets/netw1.jpg){: width="auto" height="auto" }

{: .text-center }
## <span style="color: orange; font-weight: bold;">Network Terminology</span>

###### In progress ***June 24, 2024***


##  <span style="color: royalblue; font-weight: bold;">What do we mean by "Network"?</span>


- A `network` is a group of interconnected devices (all connected to the same Wi-Fi network) that exchange data and resources together. Most notably, they share an internet connection. This can be within complicated `VLAN` network, which is a *Virtual LAN within a LAN*, or a Network could be described as a home network with common household items such as **smartphones**, **laptops**, **printers**, **smart devices**, **TV's** and **other devices**.

## Common Network infrastructure devices
- ISP modem

- Router

- Access point

- Switch

## Firewalls

- a Firewall is similar to a sifter used in baking. We want the fine particles of flour to be allowed into our dough, however we will stop big chunks and unwanted remnants from passing into the dough making by use of selective filtering.


-Specifically, a well set up firewall will block all connections. It will only allow explicitly specified types of traffic to flow IN and OUT bound. 
-An example of this could be a firewall allowing HTTPS and not HTTP. For security reasons, not allowing HTTP traffic outbound, could stop a phishing attack or credential harvesting.

- Firewalls catch and filter certain data. Many types of firewalls are implemented. Here is a short list of some examples:
- a WAF (web application firewall), protects web-based applications
- a Cloud Firewall, protects data transfer in cloud enviroments
- multiple firewalls can be used in conjunction to more efficently route data, as well as having a layered network management. 

- what do Firewall rules look like? 
-Typically, firewall rules are very complicated. They require prior knowledge of the existing firewall rules. Common fields will include; Name, Description, Interface, Allow/Deny, Source IP/group, Destination IP/Group, Ports, and profiles. 

PowerShell Ex:
> FirewallRule1 -DisplayName "Allow HTTPS" - Direction Inbound  -Protocol -TCP -LocalPort 80 -Action Allow


### Why is seperating devices so important? 



- Not all devices should have the ability to reach a `Domain Controller` or a `Medical Device` or a `Manufacturing Sensor`.

- When we look at at the reason for a subnet, partially it is to divide a network into smaller, more efficient networks.

- Another reason could be to seperate physical areas and regions such as a engineering department, sales group, 1st, 2nd, 3rd floor, and so on.

## Guest Network
- a Guest Network will be a seperate network

## VLAN
- a `VLAN` stands for Virtual Local Area Network. This is a logical segmentation configured on a network switch. This is commonly used for seperating different areas of business such as IT and HR for a company or different departments like a surgical ward and medical offices in a hospital


## DMZ

- a `DMZ` or de-militarized zone, is a subnet or `sub-network` that seperates a `LAN` Local area network, from untrusted networks or devices. 

- Usually a DMZ will face outwards, protecting the business enviroment and internal LANs. 

