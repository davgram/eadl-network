---
title: Windows workstation (AD join)
nav_order: 2
---

# Windows workstation (AD join)

Goal: Build a Windows 11 Enterprise workstation named eadl-win-client, give it a static IP on the lab NAT network, point DNS to the domain controller, and join the domain corp.eadl-dc.com. [file:55]

## Prerequisites

- Active Directory baseline completed on eadl-dc (10.0.0.5) with DNS and forwarder configured. [file:55]  
- VirtualBox NAT Network “eadl-network” (10.0.0.0/24, gateway 10.0.0.1) available. [file:55]  
- Windows 11 Enterprise ISO downloaded. [file:55]

## 1) Create the VM

- Name: eadl-win-client, 2 vCPU, 4 GB RAM, 80 GB disk, Attach to NAT Network: eadl-network, Adapter type: Intel PRO/1000 MT Desktop, Cable connected. [file:55]  
![VM settings (NIC on eadl-network)](../assets/images/win/01-vbox-settings.png) [file:55]

## 2) Install Windows 11

- Mount the Windows 11 Enterprise ISO and perform a standard installation with default partitions. [file:55]  
![Windows 11 install (select image/edition)](../assets/images/win/02-win11-install.png) [file:55]  
![Disk partitions created automatically](../assets/images/win/03-win11-disk.png) [file:55]

## 3) Set hostname and reboot

- In Windows, rename the computer to eadl-win-client and reboot to apply. [file:55]  
