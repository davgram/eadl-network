<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>EADL — Enterprise Attack Detection Lab</title>
<style>
  :root{
    --bg:#ffffff;--muted:#f8fafc;--border:#e5e7eb;--text:#0f172a;--sub:#475569;
    --brand:#2563eb;--brand-2:#22c55e;--chip:#eef2ff;--chip2:#ecfdf5;
  }
  html,body{margin:0;background:var(--bg);color:var(--text);font-family:system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Cantarell,"Helvetica Neue",Arial,"Apple Color Emoji","Segoe UI Emoji";line-height:1.45;}
  a{color:var(--brand);text-decoration:none;}
  /* Layout */
  .page{display:grid;grid-template-columns:260px 1fr;gap:0;}
  @media (max-width: 980px){.page{grid-template-columns:1fr}.sidebar{position:static;width:auto;height:auto}.content{padding-left:16px}}
  /* Sidebar */
  .sidebar{
    position:fixed;top:0;left:0;height:100vh;width:260px;border-right:1px solid var(--border);
    background:linear-gradient(180deg,#f8fafc,#ffffff 50%);overflow:auto;scrollbar-width:thin;
  }
  .brand{
    padding:14px 14px 12px 14px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:10px;
    background:linear-gradient(90deg,#38bdf8,#22c55e,#a78bfa);
    -webkit-background-clip:text;background-clip:text;color:transparent;font-weight:800;font-size:18px;
  }
  .nav{
    padding:10px 10px 18px 10px;
  }
  .nav .group-title{font-size:12px;color:var(--sub);text-transform:uppercase;letter-spacing:.08em;margin:10px 8px;}
  .link{
    display:block;border:1px solid var(--border);border-radius:10px;padding:10px 12px;margin:8px;transition:.15s background,.15s border;
    color:var(--text);background:#fff;
  }
  .link:hover{background:#f8fafc;border-color:#cbd5e1}
  .link b{font-weight:800}
  .hint{display:block;color:var(--sub);font-size:12px;margin-top:4px}
  /* Content */
  .content{margin-left:260px;padding:18px 22px;max-width:1100px}
  .hero{border:1px solid var(--border);border-radius:14px;overflow:hidden;box-shadow:0 4px 18px rgba(2,6,23,.06);margin:6px 0 18px 0}
  .hero-top{height:8px;background:linear-gradient(90deg,#0ea5e9,#22c55e,#a855f7)}
  .hero-body{display:grid;grid-template-columns:10px 1fr;background:linear-gradient(180deg,#f8fafc,#ffffff)}
  .hero-bar{background:linear-gradient(180deg,#0ea5e9,#22c55e)}
  .hero-inner{padding:16px 18px 18px 16px}
  .chips{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
  .chip{border:1px solid var(--border);background:#fff;padding:6px 10px;border-radius:999px;font-size:12px}
  .note{border-left:4px solid #f59e0b;background:#fffbea;padding:8px 10px;border-radius:6px;margin-top:10px}
  /* Section blocks */
  section{scroll-margin-top:14px}
  .card{border:1px solid var(--border);border-radius:12px;background:var(--muted);padding:16px 16px;margin:10px 0 16px 0}
  /* Tables */
  table{border-collapse:collapse;width:100%;font-size:14px}
  th,td{padding:8px 6px;border-bottom:1px solid #eaeef3;text-align:left}
  /* Utilities */
  .row{display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
  .badges{display:flex;gap:6px;flex-wrap:wrap}
  .badge{border:1px solid var(--border);border-radius:999px;padding:4px 8px;font-size:12px}
  /* Smooth scroll */
  html{scroll-behavior:smooth}
</style>
</head>
<body>

<div class="page">
  <!-- Fixed left navbar -->
  <aside class="sidebar">
    <div class="brand">EADL Navigation</div>
    <nav class="nav">
      <div class="group-title">Overview</div>
      <a class="link" href="#overview"><b>Intro</b><span class="hint">Project summary and quick facts</span></a>
      <a class="link" href="#topology"><b>Topology</b><span class="hint">Network diagram</span></a>
      <a class="link" href="#config"><b>Configuration</b><span class="hint">Hosts, specs, network, accounts</span></a>
      <a class="link" href="#evidence"><b>Evidence</b><span class="hint">Key screenshots</span></a>

      <div class="group-title">Sections</div>
      <a class="link" href="#s01"><b>01 — AD baseline</b><span class="hint">Install AD DS/DNS/DHCP</span></a>
      <a class="link" href="#s02"><b>02 — Windows workstation</b><span class="hint">Join domain, validate GPO</span></a>
      <a class="link" href="#s03"><b>03 — Linux workstation</b><span class="hint">Winbind + Kerberos</span></a>
      <a class="link" href="#s04"><b>04 — Corp server & MailHog</b><span class="hint">Mail stack for testing</span></a>
      <a class="link" href="#s05"><b>05 — Security Onion desktop</b><span class="hint">Analyst tooling</span></a>
      <a class="link" href="#s06"><b>06 — Security server (sec‑box)</b><span class="hint">Prep and hardening</span></a>
      <a class="link" href="#s07"><b>07 — Wazuh manager install</b><span class="hint">Indexer + dashboard</span></a>
      <a class="link" href="#s08"><b>08 — Enroll Wazuh agents</b><span class="hint">Windows/Linux agents</span></a>
      <a class="link" href="#s09"><b>09 — Wazuh groups & agent.conf</b><span class="hint">FIM, Sysmon, auditd</span></a>
      <a class="link" href="#s10"><b>10 — Users & snapshots</b><span class="hint">Shares and golden states</span></a>
      <a class="link" href="#s11"><b>11 — Attacker & simulation</b><span class="hint">Run and validate detections</span></a>
    </nav>
  </aside>

  <!-- Right content -->
  <main class="content">
    <!-- Hero -->
    <div class="hero" id="overview">
      <div class="hero-top"></div>
      <div class="hero-body">
        <div class="hero-bar"></div>
        <div class="hero-inner">
          <div class="row">
            <h1 style="margin:0;font-size:28px;line-height:1.15;letter-spacing:.2px;">
              Enterprise Attack Detection Lab <span style="opacity:.55;font-weight:600;">(EADL)</span>
            </h1>
            <div class="badges">
              <a href="#sections" class="badge" style="background:#ecfdf5;color:#065f46">Explore sections</a>
              <a href="./assets/images/topology.png" class="badge" style="background:#eff6ff;color:#1d4ed8">View topology</a>
            </div>
          </div>
          <p style="margin:8px 0 0 0;color:#334155;">
            Build a realistic mini‑enterprise: domain controller, Windows/Linux clients, Wazuh XDR, and Security Onion for network analysis—then attack, detect, and document with screenshots and configs recruiters can verify fast.
          </p>
          <div class="chips">
            <div class="chip">AD domain: <b>corp.eadl-dc.com</b></div>
            <div class="chip">Hosts: <b>6</b></div>
            <div class="chip">Detections: <b>attack &amp; defend</b></div>
          </div>
        </div>
      </div>
    </div>

    <!-- Author bar -->
    <div class="card">
      <div class="row">
        <div style="font-weight:700">Created by: Davide Gramuglia — SOC analyst–oriented lab showcasing AD, Linux, SIEM, and detection workflows.</div>
        <div class="badges">
          <a href="YOUR-LINKEDIN-URL" target="_blank" rel="noopener" class="badge" style="background:#ffffff">LinkedIn</a>
          <a href="YOUR-GITHUB-URL" target="_blank" rel="noopener" class="badge" style="background:#ffffff">GitHub</a>
        </div>
      </div>
    </div>

    <!-- Topology -->
    <section id="topology">
      <h3 style="margin:10px 0 8px 0;">Topology</h3>
      <div class="card" style="padding:10px">
        <p align="center" style="margin:8px 0;">
          <img src="./assets/images/topology.png" alt="EADL enterprise topology diagram" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">
        </p>
        <p style="margin:6px 0 0 0;">The diagram shows the NAT network, DC, clients, Wazuh, Security Onion, and the corporate server for a concise enterprise simulation.</p>
      </div>
    </section>

    <!-- Configuration summary -->
    <section id="config">
      <h3 style="margin:14px 0 8px 0;">Configuration summary</h3>

      <div class="card">
        <h4 style="margin:0 0 6px 0;">Hosts</h4>
        <table>
          <thead><tr><th>Hostname</th><th>IP Address</th><th>Function</th></tr></thead>
          <tbody>
            <tr><td>eadl-dc</td><td>10.0.0.5</td><td>Domain Controller (AD DS, DNS, DHCP)</td></tr>
            <tr><td>eadl-win-client</td><td>10.0.0.100</td><td>Windows Workstation (domain‑joined)</td></tr>
            <tr><td>eadl-linux-client</td><td>10.0.0.101</td><td>Linux Desktop (AD‑joined via Winbind)</td></tr>
            <tr><td>eadl-corp-svr</td><td>10.0.0.8</td><td>Corporate Server (MailHog)</td></tr>
            <tr><td>sec-box</td><td>10.0.0.10</td><td>Wazuh Manager (SIEM)</td></tr>
            <tr><td>eadl-sec-work</td><td>10.0.0.103</td><td>Security Onion desktop (NSM/analysis)</td></tr>
          </tbody>
        </table>
      </div>

      <div class="card">
        <h4 style="margin:0 0 6px 0;">VM specs</h4>
        <table>
          <thead><tr><th>VM Name</th><th>Operating System</th><th>Specs</th><th>Storage (min)</th></tr></thead>
          <tbody>
            <tr><td>eadl-dc</td><td>Windows Server 2025</td><td>2 CPU / 4096 MB</td><td>50 GB</td></tr>
            <tr><td>eadl-win-client</td><td>Windows 11 Enterprise</td><td>2 CPU / 4096 MB</td><td>80 GB</td></tr>
            <tr><td>eadl-linux-client</td><td>Ubuntu 22.04 Desktop</td><td>1 CPU / 2048 MB</td><td>80 GB</td></tr>
            <tr><td>eadl-sec-work</td><td>Security Onion 2.4.x</td><td>1 CPU / 2048 MB</td><td>55 GB</td></tr>
            <tr><td>sec-box</td><td>Ubuntu 22.04 Desktop</td><td>2 CPU / 4096 MB</td><td>80 GB</td></tr>
            <tr><td>eadl-corp-svr</td><td>Ubuntu 22.04 Server</td><td>1 CPU / 2048 MB</td><td>25 GB</td></tr>
          </tbody>
        </table>
      </div>

      <div class="card">
        <h4 style="margin:0 0 6px 0;">Core network</h4>
        <table>
          <thead><tr><th>Setting</th><th>Value</th></tr></thead>
          <tbody>
            <tr><td>VirtualBox NAT network name</td><td>eadl-network</td></tr>
            <tr><td>Subnet / Gateway</td><td>10.0.0.0/24, gw 10.0.0.1</td></tr>
            <tr><td>AD Domain</td><td>corp.eadl-dc.com</td></tr>
            <tr><td>DC DNS forwarder</td><td>8.8.8.8</td></tr>
            <tr><td>DHCP scope (lab)</td><td>10.0.0.100–10.0.0.200</td></tr>
          </tbody>
        </table>
      </div>

      <div class="card">
        <h4 style="margin:0 0 6px 0;">Accounts (public‑safe placeholders)</h4>
        <table>
          <thead><tr><th>Account</th><th>Password</th><th>Host</th></tr></thead>
          <tbody>
            <tr><td>Domain Administrator</td><td>[REDACTED]</td><td>eadl-dc</td></tr>
            <tr><td>Windows client user (domain)</td><td>[REDACTED]</td><td>eadl-win-client</td></tr>
            <tr><td>Linux client user (domain)</td><td>[REDACTED]</td><td>eadl-linux-client</td></tr>
            <tr><td>Corp server admin</td><td>[REDACTED]</td><td>eadl-corp-svr</td></tr>
            <tr><td>Wazuh admin</td><td>[REDACTED]</td><td>sec-box</td></tr>
            <tr><td>Security Onion workstation</td><td>[REDACTED]</td><td>eadl-sec-work</td></tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- Evidence -->
    <section id="evidence">
      <h3 style="margin:14px 0 8px 0;">Evidence gallery</h3>
      <div class="card">
        <ul style="margin:0 0 10px 16px;">
          <li>Domain join (Windows): <img src="./assets/images/win-join.png" alt="Windows domain join success" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
          <li>Domain join (Linux): <img src="./assets/images/linux-join.png" alt="Linux domain join success via Winbind" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
          <li>Wazuh manager dashboard: <img src="./assets/images/wazuh-ui.png" alt="Wazuh dashboard" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
          <li>Security Onion desktop: <img src="./assets/images/so-desktop.png" alt="Security Onion desktop" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
          <li>MailHog UI: <img src="./assets/images/mailhog-ui.png" alt="MailHog web UI" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;"></li>
        </ul>
      </div>
    </section>

    <!-- Sections content anchors (for left nav) -->
    <section id="sections" class="card" style="background:#ffffff">
      <h3 style="margin:0 0 8px 0;">Sections</h3>
      <p style="margin:0;color:#475569">Jump using the left navbar; anchors below are targets for deep links.</p>
    </section>

    <section id="s01" class="card"><h4 style="margin:0 0 6px 0;">01 — Active Directory baseline</h4><p style="margin:0">Install Windows Server, configure AD DS/DNS/DHCP, and prepare the lab domain.</p></section>
    <section id="s02" class="card"><h4 style="margin:0 0 6px 0;">02 — Windows workstation</h4><p style="margin:0">Join Windows 11 to the domain and verify GPO, DNS, and logon.</p></section>
    <section id="s03" class="card"><h4 style="margin:0 0 6px 0;">03 — Linux workstation</h4><p style="margin:0">Join Ubuntu via Winbind + Kerberos; test domain logins and id mapping.</p></section>
    <section id="s04" class="card"><h4 style="margin:0 0 6px 0;">04 — Corporate server &amp; MailHog</h4><p style="margin:0">Deploy lab mail stack for phishing and alerting exercises.</p></section>
    <section id="s05" class="card"><h4 style="margin:0 0 6px 0;">05 — Security Onion desktop</h4><p style="margin:0">Use analyst workstation to explore Zeek/Suricata logs and detections.</p></section>
    <section id="s06" class="card"><h4 style="margin:0 0 6px 0;">06 — Security server (sec‑box) prep</h4><p style="margin:0">Harden Ubuntu base, expand disk, and prepare for Wazuh.</p></section>
    <section id="s07" class="card"><h4 style="margin:0 0 6px 0;">07 — Wazuh manager install</h4><p style="margin:0">Install Wazuh, configure indexer and dashboard, validate health.</p></section>
    <section id="s08" class="card"><h4 style="margin:0 0 6px 0;">08 — Enroll Wazuh agents</h4><p style="margin:0">Enroll Windows/Linux agents and verify connectivity and logs.</p></section>
    <section id="s09" class="card"><h4 style="margin:0 0 6px 0;">09 — Wazuh groups &amp; agent.conf</h4><p style="margin:0">Create Windows/Linux groups; push FIM, Sysmon, and auditd configs.</p></section>
    <section id="s10" class="card"><h4 style="margin:0 0 6px 0;">10 — Users, mapping &amp; snapshots</h4><p style="margin:0">Create domain users, map shares, and snapshot golden states.</p></section>
    <section id="s11" class="card"><h4 style="margin:0 0 6px 0;">11 — Optional: Attacker &amp; simulation</h4><p style="margin:0">Run controlled attacks and validate detection coverage.</p></section>

    <div style="height:24px"></div>
  </main>
</div>

</body>
</html>
