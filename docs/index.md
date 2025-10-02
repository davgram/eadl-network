# Enterprise Attack Detection Lab (EADL)

A practical enterprise network simulation with AD DS, Windows and Linux endpoints, a corporate server running MailHog, Security Onion for analysis, and Wazuh for endpoint logging and detection. [file:55]

### Configuration summary

#### Hosts
| Hostname | IP Address | Function |
|---|---|---|
| eadl-dc | 10.0.0.5 | Domain Controller (AD DS, DNS, DHCP) |
| eadl-win-client | 10.0.0.100 | Windows Workstation (domain‑joined) |
| eadl-linux-client | 10.0.0.101 | Linux Desktop (AD‑joined via Winbind) |
| eadl-corp-svr | 10.0.0.8 | Corporate Server (MailHog) |
| sec-box | 10.0.0.10 | Wazuh Manager (SIEM) |
| eadl-sec-work | 10.0.0.103 | Security Onion desktop (NSM/analysis) |
[file:55]

#### VM specs
| VM Name | Operating System | Specs | Storage (min) |
|---|---|---|---|
| eadl-dc | Windows Server 2025 | 2 CPU / 4096 MB | 50 GB |
| eadl-win-client | Windows 11 Enterprise | 2 CPU / 4096 MB | 80 GB |
| eadl-linux-client | Ubuntu 22.04 Desktop | 1 CPU / 2048 MB | 80 GB |
| eadl-sec-work | Security Onion 2.4.x | 1 CPU / 2048 MB | 55 GB |
| sec-box | Ubuntu 22.04 Desktop | 2 CPU / 4096 MB | 80 GB |
| eadl-corp-svr | Ubuntu 22.04 Server | 1 CPU / 2048 MB | 25 GB |
[file:55]

#### Core network
| Setting | Value |
|---|---|
| VirtualBox NAT network name | eadl-network |
| Subnet / Gateway | 10.0.0.0/24, gw 10.0.0.1 |
| AD Domain | corp.eadl-dc.com |
| DC DNS forwarder | 8.8.8.8 |
| DHCP scope (lab) | 10.0.0.100–10.0.0.200 |
[file:55]

#### Services and ports
| Component | Host | Ports | Purpose |
|---|---|---|---|
| AD DS + DNS + DHCP | eadl-dc | role defaults | Identity, DNS, optional DHCP |
| Wazuh Manager 4.13.x | sec-box | 8443 (UI), agent defaults | Central agent enrollment and log collection |
| Wazuh agents | eadl-win-client, eadl-linux-client | agent channels | Windows Security/Application; Linux auth/audit |
| MailHog (Docker) | eadl-corp-svr | 1025 (SMTP), 8025 (Web UI) | Test email service and UI |
| Security Onion desktop | eadl-sec-work | desktop tools | NSM/analysis inside lab |
[file:55]

> Security note: redact real passwords in public docs and use placeholders; keep any secrets outside the repository. [file:55]

---

## Sections

- [Build enterprise network](sections/01-build-enterprise-network.md) [file:55]  
- [Active Directory setup](sections/02-active-directory-setup.md) [file:55]  
- [Windows client](sections/03-windows-client.md) [file:55]  
- [Linux client AD join](sections/04-linux-client-ad-join.md) [file:55]  
- [Corporate server & MailHog](sections/05-corp-server-mailhog.md) [file:55]  
- [Security Onion](sections/06-security-onion.md) [file:55]  
- [Wazuh manager & agents](sections/07-wazuh-manager-agents.md) [file:55]  
- [Agent group configs](sections/08-agents-group-configs.md) [file:55]  
- [Snapshots & baselines](sections/09-snapshots-and-baselines.md) [file:55]
