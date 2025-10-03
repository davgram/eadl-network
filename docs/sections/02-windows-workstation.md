---
title: Windows workstation (AD join)
nav_order: 2
---

# Windows workstation (AD join)

So now lets create a Workstations that acts like as a realistic employee endpoint, joined the domain. Ready to be monitored, attacked


Goal: Build a Windows 11 Enterprise workstation named eadl-win-client, give it a static IP on the lab NAT network, point DNS to the domain controller, and join the domain corp.eadl-dc.com.

## Prerequisites

- Active Directory baseline completed on eadl-dc (10.0.0.5) with DNS and forwarder configured.   
- VirtualBox NAT Network “eadl-network” (10.0.0.0/24, gateway 10.0.0.1) available. 
- Windows 11 Enterprise ISO downloaded. 

## 1) Create the VM
Lets go to Virtual Box Creating a new VM with Windows 11, same specs as before.
- Name: eadl-win-client, 2 vCPU, 4 GB RAM, 80 GB disk

<img src="../assets/images/windowsworkstation/createvm.png" alt="VBox NIC on eadl-network" width="800">


## 2) Install Windows 11 + Host-Only

- Mount the Windows 11 Enterprise ISO and perform a standard installation with default partitions. 
Then after the installation is completed, because its a lab i im adding any email to sign up
to do so i configured just for now the network adpater in Host Only Adapter and then i run those command as shown in the image beloiw:
 press shift f10 to open the cmd 

<img src="../assets/images/windowsworkstation/skipemail.png" alt="VBox NIC on eadl-network" width="800">


## 3) Set hostname and reboot

- In Windows, rename the computer to eadl-win-client and reboot to apply. [file:55]  
