<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>EADL — Enterprise Attack Detection Lab</title>
<style>
  :root{
    --bg:#ffffff;--muted:#f8fafc;--border:#e5e7eb;--text:#0f172a;--sub:#475569;
    --brand:#2563eb;--accent:#22c55e;
  }
  html,body{margin:0;background:var(--bg);color:var(--text);font-family:system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Cantarell,Arial;line-height:1.5;}
  a{color:var(--brand);text-decoration:none}
  /* Layout */
  .wrap{display:flex;min-height:100vh}
  .side{
    position:sticky;top:0;align-self:flex-start;
    width:260px;min-width:260px;max-height:100vh;overflow:auto;
    border-right:1px solid var(--border);background:linear-gradient(180deg,#f8fafc,#fff);
  }
  .main{flex:1;min-width:0;padding:18px}
  @media (max-width: 960px){
    .wrap{flex-direction:column}
    .side{position:static;width:auto;min-width:0;max-height:none;border-right:none;border-bottom:1px solid var(--border)}
  }
  /* Sidebar nav */
  .brand{padding:14px 14px 12px 14px;border-bottom:1px solid var(--border);font-weight:800}
  .brand span{background:linear-gradient(90deg,#38bdf8,#22c55e,#a78bfa);-webkit-background-clip:text;background-clip:text;color:transparent}
  .nav{padding:10px}
  .group{margin:10px 8px 6px 8px;font-size:12px;color:var(--sub);text-transform:uppercase;letter-spacing:.06em}
  .link{display:block;margin:8px;border:1px solid var(--border);border-radius:10px;padding:10px 12px;background:#fff;color:var(--text)}
  .link:hover{background:#f8fafc;border-color:#cbd5e1}
  .hint{display:block;color:var(--sub);font-size:12px;margin-top:4px}
  /* Content blocks */
  .hero{border:1px solid var(--border);border-radius:14px;overflow:hidden;margin:6px 0 18px 0;box-shadow:0 4px 18px rgba(2,6,23,.06)}
  .strip{height:8px;background:linear-gradient(90deg,#0ea5e9,#22c55e,#a855f7)}
  .hero-body{padding:16px}
  .chips{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
  .chip{border:1px solid var(--border);background:#fff;padding:6px 10px;border-radius:999px;font-size:12px}
  .card{border:1px solid var(--border);border-radius:12px;background:#fff;padding:14px;margin:10px 0 16px 0}
  .muted{background:var(--muted)}
  table{border-collapse:collapse;width:100%;font-size:14px}
  th,td{padding:8px 6px;border-bottom:1px solid #eaeef3;text-align:left}
  html{scroll-behavior:smooth}
</style>
</head>
<body>

<div class="wrap">
  <!-- Fixed/Sticky left navbar -->
  <aside class="side">
    <div class="brand"><span>EADL</span> Navigation</div>
    <nav class="nav">
      <div class="group">Overview</div>
      <a class="link" href="#intro"><b>Intro</b><span class="hint">Summary and quick facts</span></a>
      <a class="link" href="#topology"><b>Topology</b><span class="hint">Network diagram</span></a>
      <a class="link" href="#config"><b>Configuration</b><span class="hint">Hosts, specs, network, accounts</span></a>
      <a class="link" href="#evidence"><b>Evidence</b><span class="hint">Screenshots</span></a>

      <div class="group">Sections</div>
      <a class="link" href="#s01"><b>01 — AD baseline</b><span class="hint">AD DS/DNS/DHCP</span></a>
      <a class="link" href="#s02"><b>02 — Windows workstation</b><span class="hint">Join + GPO</span></a>
      <a class="link" href="#s03"><b>03 — Linux workstation</b><span class="hint">Winbind + Kerberos</span></a>
      <a class="link" href="#s04"><b>04 — Corp server & MailHog</b><span class="hint">Mail stack</span></a>
      <a class="link" href="#s05"><b>05 — Security Onion desktop</b><span class="hint">Analyst tooling</span></a>
      <a class="link" href="#s06"><b>06 — Security server (sec‑box)</b><span class="hint">Prep</span></a>
      <a class="link" href="#s07"><b>07 — Wazuh manager</b><span class="hint">Install</span></a>
      <a class="link" href="#s08"><b>08 — Enroll agents</b><span class="hint">Windows/Linux</span></a>
      <a class="link" href="#s09"><b>09 — Groups & agent.conf</b><span class="hint">FIM, Sysmon</span></a>
      <a class="link" href="#s10"><b>10 — Users & snapshots</b><span class="hint">Shares + golden</span></a>
      <a class="link" href="#s11"><b>11 — Attacker & simulation</b><span class="hint">Detections</span></a>
    </nav>
  </aside>

  <!-- Right content -->
  <main class="main">
    <!-- Hero -->
    <div class="hero" id="intro">
      <div class="strip"></div>
      <div class="hero-body">
        <h1 style="margin:0 0 6px 0;">Enterprise Attack Detection Lab <span style="opacity:.55;font-weight:600">(EADL)</span></h1>
        <p style="margin:6px 0 0 0;color:#334155;">
          Build a realistic mini‑enterprise: domain controller, Windows/Linux clients, Wazuh XDR, and Security Onion—then attack, detect, and document with verifiable evidence.
        </p>
        <div class="chips">
          <div class="chip">AD domain: <b>corp.eadl-dc.com</b></div>
          <div class="chip">Hosts: <b>6</b></div>
          <div class="chip">Detections: <b>attack &amp; defend</b></div>
        </div>
      </div>
    </div>

    <!-- Author -->
    <div class="card muted">
      <div style="display:flex;justify-content:space-between;gap:10px;flex-wrap:wrap;align-items:center;">
        <div style="font-weight:700">Created by: Davide Gramuglia — SOC analyst–oriented lab showcasing AD, Linux, SIEM, and detection workflows.</div>
        <div style="display:flex;gap:8px;flex-wrap:wrap;">
          <a href="YOUR-LINKEDIN-URL" class="chip" style="background:#fff">LinkedIn</a>
          <a href="YOUR-GITHUB-URL" class="chip" style="background:#fff">GitHub</a>
        </div>
      </div>
    </div>

    <!-- Topology -->
    <section id="topology" class="card">
      <h3 style="margin:0 0 8px 0;">Topology</h3>
      <p align="center" style="margin:8px 0;">
        <img src="./assets/images/topology.png" alt="EADL enterprise topology diagram" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px">
      </p>
      <p style="margin:6px 0 0 0;">NAT network with DC, Windows/Linux clients, Wazuh manager, Security Onion, and a corporate server.</p>
    </section>

    <!-- Configuration -->
    <section id="config">
      <div class="card">
        <h3 style="margin:0 0 8px 0;">Configuration summary</h3>
        <h4 style="margin:10px 0 6px 0;">Hosts</h4>
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
    <section id="evidence" class="card">
      <h3 style="margin:0 0 8px 0;">Evidence gallery</h3>
      <ul style="margin:0 0 10px 16px;">
        <li>Domain join (Windows): <img src="./assets/images/win-join.png" alt="Windows domain join success" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
        <li>Domain join (Linux): <img src="./assets/images/linux-join.png" alt="Linux domain join success via Winbind" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
        <li>Wazuh manager dashboard: <img src="./assets/images/wazuh-ui.png" alt="Wazuh dashboard" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
        <li>Security Onion desktop: <img src="./assets/images/so-desktop.png" alt="Security Onion desktop" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
        <li>MailHog UI: <img src="./assets/images/mailhog-ui.png" alt="MailHog web UI" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
      </ul>
    </section>

    <!-- Section anchors -->
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

    <div style="height:28px"></div>
  </main>
</div>

</body>
</html>
