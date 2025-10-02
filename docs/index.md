# Enterprise Attack Detection Lab (EADL)

## Configuration summary
### Configuration summary
Hosts (paste this)
Hostname	IP Address	Function
eadl-dc	10.0.0.5	Domain Controller (AD DS, DNS, DHCP)
eadl-win-client	10.0.0.100	Windows Workstation (domain-joined)
eadl-linux-client	10.0.0.101	Linux Desktop (AD-joined via Winbind)
eadl-corp-svr	10.0.0.8	Corporate Server (MailHog)
sec-box	10.0.0.10	Wazuh Manager (SIEM)
eadl-sec-work	10.0.0.103	Security Onion desktop (NSM/analysis)
Accounts and credentials (public-safe placeholders)
Account	Password	Host
Domain Administrator	[REDACTED]	eadl-dc
Win client user (domain)	[REDACTED]	eadl-win-client
Linux client user (domain)	[REDACTED]	eadl-linux-client
Corp server admin	[REDACTED]	eadl-corp-svr
Wazuh admin	[REDACTED]	sec-box
SO workstation user	[REDACTED]	eadl-sec-work
VM specs (paste this)
VM Name	Operating System	Specs	Storage (min)
eadl-dc	Windows Server 2025	2 CPU / 4096 MB	50 GB
eadl-win-client	Windows 11 Enterprise	2 CPU / 4096 MB	80 GB
eadl-linux-client	Ubuntu 22.04 Desktop	1 CPU / 2048 MB	80 GB
eadl-sec-work	Security Onion 2.4.x	1 CPU / 2048 MB	55 GB
sec-box	Ubuntu 22.04 Desktop	2 CPU / 4096 MB	80 GB
eadl-corp-svr	Ubuntu 22.04 Server	1 CPU / 2048 MB	25 GB
Core network (paste this)
Setting	Value
VirtualBox NAT network name	eadl-network
Subnet / Gateway	10.0.0.0/24, gw 10.0.0.1
AD Domain	corp.eadl-dc.com
DC DNS forwarder	8.8.8.8
DHCP scope (lab)	10.0.0.100–10.0.0.200


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
