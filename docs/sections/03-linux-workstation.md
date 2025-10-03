---
title: Linux workstation (AD join)
nav_order: 3
---

[← Back to index](../index.md){: .btn .btn-blue }

# Linux workstation (AD join)

Goal: Build an Ubuntu 22.04 Desktop workstation named `eadl-linux-client`, give it a static IP on the lab NAT network, point DNS to the domain controller, and join the domain `corp.eadl-dc.com` using Samba/Winbind. [file:55]

## Prerequisites

- Active Directory baseline is online on `eadl-dc (10.0.0.5)` with DNS and a forwarder configured. [file:55]  
- VirtualBox NAT Network `eadl-network (10.0.0.0/24, gateway 10.0.0.1)` exists and is used by all VMs. [file:55]  
- Ubuntu 22.04.5 Desktop ISO downloaded to the host. [file:55]

## 1) Create the VM (VirtualBox)

- Name: `eadl-linux-client`, `2 vCPU`, `2 GB RAM`, `25 GB` disk; attach Adapter 1 to NAT Network → Name: `eadl-network`; Adapter type: Intel PRO/1000 MT Desktop; Cable connected. [file:55]

<details>
  <summary><strong>Click to show screenshot</strong></summary>
  <img src="../assets/images/linuxworkstation/01-vbox-create.png" alt="Create Ubuntu VM on eadl-network" width="850">
</details>

## 2) Install Ubuntu 22.04 Desktop

- Proceed with the standard installer; sample unattended values used in notes: real name “Sam Wilson”, username `samw`, password `password123@` (weak on purpose for lab). [file:55]  
- After first boot, set Power → Blank screen “Never” to avoid session drops during lab work. [file:55]

<details>
  <summary><strong>Click to show screenshot</strong></summary>
  <img src="../assets/images/linuxworkstation/02-install-ubuntu.png" alt="Ubuntu installer" width="850">
</details>

## 3) Configure network (static IP + DNS)

- Set static IPv4 and DNS so AD lookups are reliable: `IP 10.0.0.101`, `Mask 255.255.255.0`, `Gateway 10.0.0.1`, `DNS 10.0.0.5`. [file:55]

<details>
  <summary><strong>Click to show screenshot</strong></summary>
  <img src="../assets/images/linuxworkstation/03-ipv4-static.png" alt="IPv4 static 10.0.0.101 / DNS 10.0.0.5" width="850">
</details>

## 4) Snapshot: baseline

- Take a snapshot “Baseline conf” so the workstation can be restored before domain join or agent installs. [file:55]

<details>
  <summary><strong>Click to show screenshot</strong></summary>
  <img src="../assets/images/linuxworkstation/04-snapshot-baseline.png" alt="Snapshot baseline" width="850">
</details>

## 5) Install Winbind stack

Update and install required packages. [file:55]
