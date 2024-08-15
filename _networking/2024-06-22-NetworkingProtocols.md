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


- A `network` is a group of interconnected computing devices or nodes, that exchange data and resources together. Most notably, they share an internet connection. This can be within a complicated `subnetted` network, which is a *network inside of a network*, or simply a home network with common things like **smartphones**, **laptops**, **printers**, **smart devices**, **TV's** and **other devices**.

### Protocols:

- a Protocol can be something for recieving and transferring, such as `https` or `sftp`. It can be also a mode of authentication or encryption like `SAML` and `SSL` for example. 

### Subnet? whats that?

- a `Subnet` is a smaller contained network within a larger network.
- one of the most common examples is a office enviroment with many floors and departments. If this is a production enviroment, a PLC or Manufacturing device would likely (and hopefully) be on a different network from a printer or laptop. 

## Firewalls

- a Firewall is similar to a sifter used in baking. We want the fine particles of flour to be allowed into our dough, however we will stop big chunks and unwanted remnants from passing into the dough making by use of the sift filtering.

- Firewalls catch and filter certain data. Many types of firewalls are implemented. Here is a short list of some examples:

- a WAF (web application firewall), protects web-based applications
- a Cloud Firewall, protects data transfer in cloud enviroments
- multiple firewalls can be used in conjunction to more efficently route data, as well as having a layered network management. 


## DMZ

- a `DMZ` or de-militarized zone, is a subnet or `sub-network` that seperates a `LAN` Local area network, from untrusted networks or devices. 

- Usually a DMZ will face outwards, protecting the business enviroment and internal LANs. 

### Why is seperating devices so important? 

- Not all devices should have the ability to talk to a `Domain Controller` or a `Medical Device`.

- When we look at at the reason for a subnet, partially it is to divide a network into smaller, more efficient networks.

- Another reason could be to seperate physical areas and regions such as a engineering department, sales group, 1st, 2nd, 3rd floor, and so on.

