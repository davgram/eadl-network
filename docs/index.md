# Enterprise Attack Detection Lab (EADL)

## Configuration summary
### Configuration summary

> This section summarizes the enterprise lab topology, core network parameters, and security stack so reviewers can understand the environment at a glance. Replace any TBD fields as the build progresses. [file:55]

#### Network inventory
| Hostname | Role | OS | IP | Notes |
|---|---|---|---|---|
| eadl-dc [file:55] | Domain Controller (AD DS, DNS, DHCP) [file:55] | Windows Server 2025 [file:55] | TBD | DNS forwarder 8.8.8.8; DHCP scope planned 10.0.0.100–200 [file:55] |
| eadl-win-client [file:55] | Domain‑joined workstation [file:55] | Windows 11 Enterprise [file:55] | TBD | Joined corp.eadl-dc.com; DNS set to DC [file:55] |
| eadl-linux-client [file:55] | Domain‑joined developer workstation [file:55] | Ubuntu 22.04.5 Desktop [file:55] | TBD | Winbind/Samba AD join; DNS 10.0.0.5 (DC) [file:55] |
| eadl-corp-svr [file:55] | Corporate server (MailHog) [file:55] | Ubuntu 22.04.5 [file:55] | TBD | Docker MailHog; SMTP 1025, Web UI 8025 [file:55] |
| eadl-sec-work [file:55] | Security Onion desktop [file:55] | Security Onion 2.4.x [file:55] | TBD | Analysis/NSM workstation on lab network [file:55] |
| sec-box [file:55] | Wazuh manager host [file:55] | Ubuntu 22.04.5 [file:55] | TBD | Wazuh 4.13.x; UI planned on 8443 (internal) [file:55] |

#### Core network settings
| Setting | Value |
|---|---|
| VirtualBox NAT network name | eadl-network [file:55] |
| Addressing | 10.0.0.0/24 (gateway 10.0.0.1) [file:55] |
| AD Domain | corp.eadl-dc.com [file:55] |
| DNS forwarder (on DC) | 8.8.8.8 [file:55] |
| DHCP scope (lab) | 10.0.0.100–10.0.0.200 (enable/authorize on DC) [file:55] |
| Client DNS | Point all lab hosts to DC first [file:55] |

#### Security stack and services
| Component | Host | Ports | Purpose |
|---|---|---|---|
| AD DS + DNS + DHCP [file:55] | eadl-dc [file:55] | standard role ports [file:55] | Identity, name resolution, IP assignment [file:55] |
| Wazuh Manager 4.13.x [file:55] | sec-box [file:55] | 8443 (UI), agent defaults [file:55] | Central agent enrollment and log collection [file:55] |
| Wazuh agents [file:55] | Windows + Linux endpoints [file:55] | agent channels [file:55] | Windows Security/Application; Linux auth/audit via groups [file:55] |
| Security Onion desktop [file:55] | eadl-sec-work [file:55] | desktop tools [file:55] | NSM/analysis inside lab network [file:55] |
| MailHog (Docker) [file:55] | eadl-corp-svr [file:55] | 1025 (SMTP), 8025 (UI) [file:55] | Test email service and ingestion [file:55] |

#### Config checklist (fill as you go)
- VirtualBox: create NAT Network “eadl-network” and attach each VM to it. [file:55]
- DC: install AD DS/DNS/DHCP, create forest corp.eadl-dc.com, set DNS forwarder 8.8.8.8. [file:55]
- DHCP: authorize scope 10.0.0.100–200 or use static IPs per host plan. [file:55]
- Clients: set DNS to DC, join domain (Windows + Linux via Winbind/Samba). [file:55]
- Wazuh: deploy manager on sec-box, enroll Windows/Linux agents into groups with centralized agent.conf. [file:55]
- MailHog: run via Docker on eadl-corp-svr, map 1025/8025, verify with test sender/poller. [file:55]
- Snapshots: take baseline, post‑AD, and post‑agent milestones to enable safe rollback. [file:55]

## Sections
- [Build enterprise network](sections/01-build-enterprise-network.md)
- [Active Directory setup](sections/02-active-directory-setup.md)
- [Windows client](sections/03-windows-client.md)
- [Linux client AD join](sections/04-linux-client-ad-join.md)
- [Corporate server & MailHog](sections/05-corp-server-mailhog.md)
- [Security Onion](sections/06-security-onion.md)
- [Wazuh manager & agents](sections/07-wazuh-manager-agents.md)
- [Agent group configs](sections/08-agents-group-configs.md)
- [Snapshots & baselines](sections/09-snapshots-and-baselines.md)
