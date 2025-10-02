# Enterprise Attack Detection Lab (EADL)

## Configuration summary
### Configuration summary
#### Hosts
| Hostname | IP Address | Function |
|---|---|---|
| eadl-dc [file:55] | 10.0.0.5 [file:55] | Domain Controller (AD DS, DNS, DHCP) [file:55] |
| eadl-win-client [file:55] | 10.0.0.100 (static) [file:55] | Windows Workstation (domain‑joined) [file:55] |
| eadl-linux-client [file:55] | 10.0.0.101 [file:55] | Linux Desktop (AD‑joined via Winbind) [file:55] |
| eadl-corp-svr [file:55] | 10.0.0.8 [file:55] | Corporate Server (MailHog) [file:55] |
| sec-box [file:55] | 10.0.0.10 [file:55] | Wazuh Manager (SIEM) [file:55] |
| eadl-sec-work [file:55] | 10.0.0.103/24 [file:55] | Security Onion desktop (NSM/analysis) [file:55] |



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
