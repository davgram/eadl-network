# Enterprise Attack Detection Lab (EADL)

<!-- Top author bar with LinkedIn -->
<div style="display:flex;justify-content:space-between;align-items:center;gap:12px;border:1px solid #e5e7eb;background:#f8fafc;padding:10px 12px;border-radius:10px;margin:6px 0 14px 0;">
  <div style="font-weight:600;">
    Created by: Davide Gramuglia — SOC analyst–oriented lab showcasing AD, Linux, SIEM, and detection workflows.
  </div>
  <a href="YOUR-LINKEDIN-URL" target="_blank" rel="noopener noreferrer" title="LinkedIn profile" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;border:1px solid #e5e7eb;padding:6px 10px;border-radius:999px;background:#ffffff;">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" width="18" height="18" aria-hidden="true"><path fill="#0a66c2" d="M100.28 448H7.4V148.9h92.88zm-46.44-340C24.86 108 0 83 0 52.9A52.9 52.9 0 0 1 53.84 0c29.5 0 53.84 24 53.84 52.9S83.33 108 53.84 108zM447.9 448h-92.4V302.4c0-34.7-.7-79.3-48.3-79.3-48.3 0-55.7 37.7-55.7 76.6V448h-92.4V148.9h88.7v40.8h1.3c12.3-23.4 42.4-48.3 87.3-48.3 93.5 0 110.7 61.5 110.7 141.4z"/></svg>
    <span style="font-weight:600;color:#0a66c2;">LinkedIn</span>
  </a>
</div>

<!-- Hero header -->
<div style="border:1px solid #e5e7eb;background:linear-gradient(180deg,#f8fafc, #ffffff);padding:18px 18px;border-radius:12px;margin:10px 0 18px 0;">
  <div style="display:flex;flex-wrap:wrap;align-items:center;gap:12px;justify-content:space-between;">
    <div style="font-size:20px;font-weight:700;line-height:1.2;">Enterprise Attack Detection Lab</div>
    <div style="display:flex;gap:6px;flex-wrap:wrap;">
      <span style="border:1px solid #e5e7eb;background:#eff6ff;color:#1d4ed8;padding:4px 8px;border-radius:999px;font-size:12px;">Active Directory</span>
      <span style="border:1px solid #e5e7eb;background:#ecfdf5;color:#065f46;padding:4px 8px;border-radius:999px;font-size:12px;">Linux</span>
      <span style="border:1px solid #e5e7eb;background:#fff7ed;color:#9a3412;padding:4px 8px;border-radius:999px;font-size:12px;">Security Onion</span>
      <span style="border:1px solid #e5e7eb;background:#fef2f2;color:#991b1b;padding:4px 8px;border-radius:999px;font-size:12px;">Wazuh</span>
      <span style="border:1px solid #e5e7eb;background:#f5f3ff;color:#5b21b6;padding:4px 8px;border-radius:999px;font-size:12px;">SIEM</span>
    </div>
  </div>
  <p style="margin:10px 0 0 0;">
    This project demonstrates enterprise‑style network design, Windows/Linux administration, and SOC workflows by building a small business network with Active Directory, a corporate server, Security Onion, and Wazuh for endpoint telemetry and detections. The goal is to document reproducible builds, clear evidence (screenshots, configs), and measurable outcomes recruiters can review quickly.
  </p>
</div>

<!-- Image tip -->
<div style="border:1px solid #e5e7eb;background:#fffbea;border-left:6px solid #f59e0b;padding:12px 14px;border-radius:8px;margin:12px 0;">
  <p style="margin:0;">
    Images: place PNG/JPG files in <code>docs/assets/images</code> and reference them with relative paths like
    <code>./assets/images/topology.png</code>. This works reliably on GitHub Pages. Do not start image paths with <code>/</code>.
  </p>
</div>

## About this project

- Why: Demonstrate practical skills for SOC/Blue Team roles—AD setup, endpoint management, logging, and analysis in a realistic lab.  
- What: VirtualBox NAT lab with a domain controller, Windows and Linux clients, a MailHog server, a Wazuh manager, and a Security Onion workstation.  
- Evidence: Build steps, configuration tables, and screenshots showing domain joins, agent enrollment, dashboards, and test data flows.

### Topology

<p align="center">
  <img src="./assets/images/topology.png" alt="EADL enterprise topology diagram" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">
</p>

<p style="margin:8px 0 0 0;">
  Add a simple diagram (draw.io/diagrams.net or screenshots) that shows the NAT network, DC, clients, Wazuh, Security Onion, and the corporate server. Save as <code>docs/assets/images/topology.png</code>.
</p>

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

#### VM specs

| VM Name | Operating System | Specs | Storage (min) |
|---|---|---|---|
| eadl-dc | Windows Server 2025 | 2 CPU / 4096 MB | 50 GB |
| eadl-win-client | Windows 11 Enterprise | 2 CPU / 4096 MB | 80 GB |
| eadl-linux-client | Ubuntu 22.04 Desktop | 1 CPU / 2048 MB | 80 GB |
| eadl-sec-work | Security Onion 2.4.x | 1 CPU / 2048 MB | 55 GB |
| sec-box | Ubuntu 22.04 Desktop | 2 CPU / 4096 MB | 80 GB |
| eadl-corp-svr | Ubuntu 22.04 Server | 1 CPU / 2048 MB | 25 GB |

#### Core network

| Setting | Value |
|---|---|
| VirtualBox NAT network name | eadl-network |
| Subnet / Gateway | 10.0.0.0/24, gw 10.0.0.1 |
| AD Domain | corp.eadl-dc.com |
| DC DNS forwarder | 8.8.8.8 |
| DHCP scope (lab) | 10.0.0.100–10.0.0.200 |

#### Accounts (public‑safe placeholders)

| Account | Password | Host |
|---|---|---|
| Domain Administrator | [REDACTED] | eadl-dc |
| Windows client user (domain) | [REDACTED] | eadl-win-client |
| Linux client user (domain) | [REDACTED] | eadl-linux-client |
| Corp server admin | [REDACTED] | eadl-corp-svr |
| Wazuh admin | [REDACTED] | sec-box |
| Security Onion workstation | [REDACTED] | eadl-sec-work |

### Evidence gallery

- Domain join (Windows): <img src="./assets/images/win-join.png" alt="Windows domain join success" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">  
- Domain join (Linux): <img src="./assets/images/linux-join.png" alt="Linux domain join success via Winbind" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">  
- Wazuh manager dashboard: <img src="./assets/images/wazuh-ui.png" alt="Wazuh dashboard" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">  
- Security Onion desktop: <img src="./assets/images/so-desktop.png" alt="Security Onion desktop" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">  
- MailHog UI: <img src="./assets/images/mailhog-ui.png" alt="MailHog web UI" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

<p style="margin:8px 0 0 0;">
  Add screenshots with filenames matching the references above into <code>docs/assets/images</code>. Use short, clear captions in the surrounding text.
</p>

---

## Sections

- [01 — Active Directory baseline](sections/01-ad-baseline.md)
- [02 — Windows workstation (AD join)](sections/02-windows-workstation.html)
- [03 — Linux workstation (AD join)](sections/03-linux-workstation.md)
- [04 — Corporate server & MailHog](sections/04-corporate-server-mailhog.md)
- [05 — Security Onion desktop](sections/05-security-onion-desktop.md)
- [06 — Security server (sec-box) prep](sections/06-security-server-sec-box.md)
- [07 — Wazuh manager install + disk expansion](sections/07-wazuh-manager-install.md)
- [08 — Enroll Wazuh agents (Win/Linux)](sections/08-wazuh-agents-enroll.md)
- [09 — Wazuh groups & agent.conf](sections/09-wazuh-groups-agentconf.md)
- [10 — Users, mapping & snapshots](sections/10-users-and-snapshots.md)
- [11 — Optional: Attacker & simulation](sections/11-attacker-simulation.md)
