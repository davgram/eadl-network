<!-- EADL: Enterprise Attack Detection Lab -->

<!-- Hero banner -->
<div style="margin:8px 0 18px 0;border-radius:14px;overflow:hidden;border:1px solid #e5e7eb;box-shadow:0 4px 18px rgba(2,6,23,.06);">
  <div style="height:8px;background:linear-gradient(90deg,#0ea5e9,#22c55e,#a855f7);"></div>

  <div style="display:grid;grid-template-columns:10px 1fr;gap:0;background:linear-gradient(180deg,#f8fafc 0%, #ffffff 100%);">
    <div style="background:linear-gradient(180deg,#0ea5e9,#22c55e);"></div>

    <div style="padding:16px 18px 18px 16px;">
      <div style="display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap;">
        <h1 style="margin:0;font-size:28px;line-height:1.15;letter-spacing:.2px;">
          Enterprise Attack Detection Lab <span style="opacity:.55;font-weight:600;">(EADL)</span>
        </h1>

        <div style="display:flex;gap:8px;flex-wrap:wrap;">
          <a href="#sections" style="text-decoration:none;border:1px solid #e5e7eb;padding:7px 10px;border-radius:8px;background:#ecfdf5;color:#065f46;font-weight:600;">Explore sections</a>
          <a href="./assets/images/topology.png" style="text-decoration:none;border:1px solid #e5e7eb;padding:7px 10px;border-radius:8px;background:#eff6ff;color:#1d4ed8;font-weight:600;">View topology</a>
        </div>
      </div>

      <p style="margin:8px 0 0 0;color:#334155;">
        Build a realistic mini‑enterprise: domain controller, Windows/Linux clients, Wazuh XDR, and Security Onion for network analysis—then attack, detect, and document with screenshots and configs recruiters can verify fast.
      </p>

      <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:10px;">
        <div style="border:1px solid #e5e7eb;background:#ffffff;padding:6px 10px;border-radius:999px;font-size:12px;">AD domain: <b>corp.eadl-dc.com</b></div>
        <div style="border:1px solid #e5e7eb;background:#ffffff;padding:6px 10px;border-radius:999px;font-size:12px;">Hosts: <b>6</b></div>
        <div style="border:1px solid #e5e7eb;background:#ffffff;padding:6px 10px;border-radius:999px;font-size:12px;">Detections: <b>attack &amp; defend</b></div>
      </div>
    </div>
  </div>
</div>

<!-- Top author bar -->
<div style="display:flex;justify-content:space-between;align-items:center;gap:12px;border:1px solid #e5e7eb;background:#f8fafc;padding:10px 12px;border-radius:10px;margin:6px 0 16px 0;">
  <div style="font-weight:700;">
    Created by: Davide Gramuglia — SOC analyst–oriented lab showcasing AD, Linux, SIEM, and detection workflows.
  </div>
  <div style="display:flex;gap:8px;align-items:center;">
    <a href="YOUR-LINKEDIN-URL" target="_blank" rel="noopener noreferrer" title="LinkedIn profile" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;border:1px solid #e5e7eb;padding:6px 10px;border-radius:999px;background:#ffffff;">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" width="18" height="18" aria-hidden="true"><path fill="#0a66c2" d="M100.28 448H7.4V148.9h92.88zm-46.44-340C24.86 108 0 83 0 52.9A52.9 52.9 0 0 1 53.84 0c29.5 0 53.84 24 53.84 52.9S83.33 108 53.84 108zM447.9 448h-92.4V302.4c0-34.7-.7-79.3-48.3-79.3-48.3 0-55.7 37.7-55.7 76.6V448h-92.4V148.9h88.7v40.8h1.3c12.3-23.4 42.4-48.3 87.3-48.3 93.5 0 110.7 61.5 110.7 141.4z"/></svg>
      <span style="font-weight:600;color:#0a66c2;">LinkedIn</span>
    </a>
    <a href="YOUR-GITHUB-URL" target="_blank" rel="noopener noreferrer" title="GitHub profile" style="display:inline-flex;align-items:center;gap:8px;text-decoration:none;border:1px solid #e5e7eb;padding:6px 10px;border-radius:999px;background:#ffffff;">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" width="18" height="18" aria-hidden="true"><path fill="#24292f" d="M8 0C3.58 0 0 3.58 0 8a8 8 0 0 0 5.47 7.59c.4.07.55-.17.55-.38..."/></svg>
      <span style="font-weight:600;color:#24292f;">GitHub</span>
    </a>
  </div>
</div>

<!-- Hero header -->
<div style="border:1px solid #e5e7eb;background:linear-gradient(180deg,#f8fafc, #ffffff);padding:18px 18px;border-radius:12px;margin:10px 0 18px 0;">
  <div style="display:flex;flex-wrap:wrap;align-items:center;gap:12px;justify-content:space-between;">
    <div style="font-size:20px;font-weight:700;line-height:1.2;">Enterprise Attack Detection Lab</div>
    <div style="display:flex;gap:6px;flex-wrap:wrap;">
      <span style="border:1px solid #e5e7eb;background:#eff6ff;color:#1d4ed8;padding:4px 8px;border-radius:999px;font-size:12px;">Active Directory</span>
      <span style="border:1px solid #e5e7eb;background:#ecfdf5;color:#065f46;padding:4px 8px;border-radius:999px;font-size:12px;">Linux</span>
      <span style="border:1px solid #e5e7eb;background:#fff7ed;color:#9a3412;padding:4px 8px;border-radius:999px;font-size:12px;">Windows</span>
      <span style="border:1px solid #e5e7eb;background:#fef2f2;color:#991b1b;padding:4px 8px;border-radius:999px;font-size:12px;">Wazuh</span>
      <span style="border:1px solid #e5e7eb;background:#f5f3ff;color:#5b21b6;padding:4px 8px;border-radius:999px;font-size:12px;">Security Onion</span>
      <span style="border:1px solid #e5e7eb;background:#e0f2fe;color:#075985;padding:4px 8px;border-radius:999px;font-size:12px;">Detection</span>
    </div>
  </div>
  <p style="margin:10px 0 0 0;">
    This project demonstrates enterprise‑style network design, Windows/Linux administration, and SOC workflows by building a small business network with Active Directory, a corporate server, Security Onion, and Wazuh for endpoint telemetry and detections. The goal is to document reproducible builds, clear evidence (screenshots, configs), and measurable outcomes recruiters can review quickly.
  </p>
</div>

<!-- Topology -->
<h3 id="topology" style="margin:16px 0 8px 0;">Topology</h3>
<p align="center" style="margin:8px 0;">
  <img src="./assets/images/topology.png" alt="EADL enterprise topology diagram" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">
</p>
<p style="margin:8px 0 0 0;">
  A simple diagram should show the NAT network, DC, clients, Wazuh, Security Onion, and the corporate server. Save as <code>docs/assets/images/topology.png</code>.
</p>

<!-- Configuration summary -->
<h3 style="margin:18px 0 10px 0;">Configuration summary</h3>

<h4 style="margin:10px 0 6px 0;">Hosts</h4>
<table style="border-collapse:collapse;width:100%;font-size:14px;">
  <thead>
    <tr>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Hostname</th>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">IP Address</th>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Function</th>
    </tr>
  </thead>
  <tbody>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-dc</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">10.0.0.5</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Domain Controller (AD DS, DNS, DHCP)</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-win-client</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">10.0.0.100</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Windows Workstation (domain‑joined)</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-linux-client</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">10.0.0.101</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Linux Desktop (AD‑joined via Winbind)</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-corp-svr</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">10.0.0.8</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Corporate Server (MailHog)</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">sec-box</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">10.0.0.10</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Wazuh Manager (SIEM)</td></tr>
    <tr><td style="padding:6px 4px;">eadl-sec-work</td><td style="padding:6px 4px;">10.0.0.103</td><td style="padding:6px 4px;">Security Onion desktop (NSM/analysis)</td></tr>
  </tbody>
</table>

<h4 style="margin:12px 0 6px 0;">VM specs</h4>
<table style="border-collapse:collapse;width:100%;font-size:14px;">
  <thead>
    <tr>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">VM Name</th>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Operating System</th>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Specs</th>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Storage (min)</th>
    </tr>
  </thead>
  <tbody>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-dc</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Windows Server 2025</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">2 CPU / 4096 MB</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">50 GB</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-win-client</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Windows 11 Enterprise</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">2 CPU / 4096 MB</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">80 GB</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-linux-client</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Ubuntu 22.04 Desktop</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">1 CPU / 2048 MB</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">80 GB</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-sec-work</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Security Onion 2.4.x</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">1 CPU / 2048 MB</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">55 GB</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">sec-box</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Ubuntu 22.04 Desktop</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">2 CPU / 4096 MB</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">80 GB</td></tr>
    <tr><td style="padding:6px 4px;">eadl-corp-svr</td><td style="padding:6px 4px;">Ubuntu 22.04 Server</td><td style="padding:6px 4px;">1 CPU / 2048 MB</td><td style="padding:6px 4px;">25 GB</td></tr>
  </tbody>
</table>

<h4 style="margin:12px 0 6px 0;">Core network</h4>
<table style="border-collapse:collapse;width:100%;font-size:14px;">
  <thead>
    <tr>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Setting</th>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Value</th>
    </tr>
  </thead>
  <tbody>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">VirtualBox NAT network name</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-network</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Subnet / Gateway</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">10.0.0.0/24, gw 10.0.0.1</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">AD Domain</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">corp.eadl-dc.com</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">DC DNS forwarder</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">8.8.8.8</td></tr>
    <tr><td style="padding:6px 4px;">DHCP scope (lab)</td><td style="padding:6px 4px;">10.0.0.100–10.0.0.200</td></tr>
  </tbody>
</table>

<h4 style="margin:12px 0 6px 0;">Accounts (public‑safe placeholders)</h4>
<table style="border-collapse:collapse;width:100%;font-size:14px;">
  <thead>
    <tr>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Account</th>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Password</th>
      <th style="text-align:left;border-bottom:1px solid #e5e7eb;padding:6px 4px;">Host</th>
    </tr>
  </thead>
  <tbody>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Domain Administrator</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">[REDACTED]</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-dc</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Windows client user (domain)</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">[REDACTED]</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-win-client</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Linux client user (domain)</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">[REDACTED]</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-linux-client</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Corp server admin</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">[REDACTED]</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">eadl-corp-svr</td></tr>
    <tr><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">Wazuh admin</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">[REDACTED]</td><td style="padding:6px 4px;border-bottom:1px solid #f1f5f9;">sec-box</td></tr>
    <tr><td style="padding:6px 4px;">Security Onion workstation</td><td style="padding:6px 4px;">[REDACTED]</td><td style="padding:6px 4px;">eadl-sec-work</td></tr>
  </tbody>
</table>

<!-- Evidence gallery -->
<h3 style="margin:18px 0 10px 0;">Evidence gallery</h3>
<ul style="margin:0 0 10px 16px;">
  <li>Domain join (Windows): <img src="./assets/images/win-join.png" alt="Windows domain join success" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
  <li>Domain join (Linux): <img src="./assets/images/linux-join.png" alt="Linux domain join success via Winbind" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
  <li>Wazuh manager dashboard: <img src="./assets/images/wazuh-ui.png" alt="Wazuh dashboard" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
  <li>Security Onion desktop: <img src="./assets/images/so-desktop.png" alt="Security Onion desktop" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
  <li>MailHog UI: <img src="./assets/images/mailhog-ui.png" alt="MailHog web UI" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
</ul>

<hr style="border:none;border-top:1px solid #e5e7eb;margin:18px 0;">

<!-- Sections: improved style -->
<h3 id="sections" style="margin:12px 0 8px 0;">Sections</h3>

<div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:12px;">
  <a href="sections/01-ad-baseline.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">01 — Active Directory baseline</div>
    <div style="color:#475569;font-size:13px;">Install Windows Server, configure AD DS/DNS/DHCP, and prepare the lab domain.</div>
  </a>

  <a href="sections/02-windows-workstation.html" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">02 — Windows workstation</div>
    <div style="color:#475569;font-size:13px;">Join Windows 11 to the domain and verify GPO, DNS, and logon.</div>
  </a>

  <a href="sections/03-linux-workstation.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">03 — Linux workstation</div>
    <div style="color:#475569;font-size:13px;">Join Ubuntu via Winbind + Kerberos; test domain logins and id mapping.</div>
  </a>

  <a href="sections/04-corporate-server-mailhog.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">04 — Corporate server &amp; MailHog</div>
    <div style="color:#475569;font-size:13px;">Deploy lab mail stack for phishing and alerting exercises.</div>
  </a>

  <a href="sections/05-security-onion-desktop.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">05 — Security Onion desktop</div>
    <div style="color:#475569;font-size:13px;">Use analyst workstation to explore Zeek/Suricata logs and detections.</div>
  </a>

  <a href="sections/06-security-server-sec-box.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">06 — Security server (sec‑box) prep</div>
    <div style="color:#475569;font-size:13px;">Harden Ubuntu base, expand disk, and prepare for Wazuh.</div>
  </a>

  <a href="sections/07-wazuh-manager-install.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">07 — Wazuh manager install</div>
    <div style="color:#475569;font-size:13px;">Install Wazuh, configure indexer and dashboard, validate health.</div>
  </a>

  <a href="sections/08-wazuh-agents-enroll.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">08 — Enroll Wazuh agents</div>
    <div style="color:#475569;font-size:13px;">Enroll Windows/Linux agents and verify connectivity and logs.</div>
  </a>

  <a href="sections/09-wazuh-groups-agentconf.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">09 — Wazuh groups &amp; agent.conf</div>
    <div style="color:#475569;font-size:13px;">Create Windows/Linux groups; push FIM, Sysmon, and auditd configs.</div>
  </a>

  <a href="sections/10-users-and-snapshots.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">10 — Users, mapping &amp; snapshots</div>
    <div style="color:#475569;font-size:13px;">Create domain users, map shares, and snapshot golden states.</div>
  </a>

  <a href="sections/11-attacker-simulation.md" style="text-decoration:none;border:1px solid #e5e7eb;border-radius:10px;padding:12px;background:#ffffff;display:block;">
    <div style="font-weight:700;margin-bottom:6px;">11 — Optional: Attacker &amp; simulation</div>
    <div style="color:#475569;font-size:13px;">Run controlled attacks and validate detection coverage.</div>
  </a>
</div>
