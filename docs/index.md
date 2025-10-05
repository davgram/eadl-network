<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>EADL — Enterprise Attack Detection Lab</title>
<style>
  :root{--nav-w:260px}
  html,body{margin:0;height:100%}
  body{font-family:system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Arial;color:#0f172a;background:#ffffff}

  a{color:#2563eb;text-decoration:none}

  /* Sidebar fixed to the true left */
  .side{
    position:fixed;z-index:20;top:0;left:0;height:100vh;width:var(--nav-w);
    border-right:1px solid #e5e7eb;background:linear-gradient(180deg,#f8fafc,#fff);
    overflow:auto;scrollbar-width:thin;
  }
  .brand{padding:14px;border-bottom:1px solid #e5e7eb;font-weight:800}
  .brand span{background:linear-gradient(90deg,#38bdf8,#22c55e,#a78bfa);-webkit-background-clip:text;background-clip:text;color:transparent}
  .nav{padding:12px}
  .nav strong{display:block;margin:0 6px 8px}
  .nav a{
    display:block;margin:8px 6px;padding:8px 10px;border:1px solid #e5e7eb;border-radius:8px;background:#fff;color:#0f172a
  }
  .nav a:hover{background:#f1f5f9}

  /* Main content shifted to make room for fixed sidebar */
  .main{
    margin-left:var(--nav-w); /* reserve space for fixed left nav */
    padding:16px 18px;max-width:1120px
  }

  /* Cards and visuals */
  .hero{border:1px solid #e5e7eb;border-radius:12px;overflow:hidden;margin:8px 0 18px;box-shadow:0 3px 16px rgba(2,6,23,.06)}
  .strip{height:6px;background:linear-gradient(90deg,#0ea5e9,#22c55e,#a855f7)}
  .hero-body{padding:16px}
  .chips{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
  .chip{border:1px solid #e5e7eb;background:#fff;padding:6px 10px;border-radius:999px;font-size:12px}
  .card{border:1px solid #e5e7eb;border-radius:10px;padding:14px;margin:10px 0 16px;background:#fff}
  table{border-collapse:collapse;width:100%;font-size:14px}
  th,td{padding:8px 6px;border-bottom:1px solid #eaeef3;text-align:left}

  /* Showcase timeline styles from previous version */
  .showcase{position:relative;border:1px solid #e5e7eb;border-radius:12px;background:linear-gradient(180deg,#f8fafc,#ffffff);padding:14px 14px 6px 14px;margin:12px 0 18px 0;box-shadow:0 6px 22px rgba(2,6,23,.06)}
  .show-head{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-bottom:6px}
  .show-title{margin:0;font-size:18px;font-weight:800;letter-spacing:.2px}
  .show-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:12px}
  .sc{position:relative;border:1px solid #e5e7eb;background:#fff;border-radius:12px;padding:12px 12px 12px 14px}
  .sc:before{content:"";position:absolute;left:-1px;top:-1px;height:4px;width:calc(100% + 2px);background:linear-gradient(90deg,#0ea5e9,#22c55e,#a855f7);border-top-left-radius:12px;border-top-right-radius:12px}
  .sc h4{margin:8px 0 4px 0;font-size:15px}
  .sc p{margin:0;color:#475569;font-size:13px}
  .meta{margin-top:8px;display:flex;gap:6px;flex-wrap:wrap}
  .tag{border:1px solid #e5e7eb;background:#ffffff;border-radius:999px;padding:3px 8px;font-size:11px;color:#334155}
  .ico{width:20px;height:20px;border-radius:6px;display:inline-flex;align-items:center;justify-content:center;margin-right:6px}
  .ico.ad{background:#eff6ff;color:#1d4ed8}.ico.win{background:#fef2f2;color:#991b1b}.ico.linux{background:#ecfdf5;color:#065f46}
  .ico.mail{background:#fff7ed;color:#9a3412}.ico.so{background:#f5f3ff;color:#5b21b6}.ico.sec{background:#e0f2fe;color:#075985}
  .ico.wz{background:#fef2f2;color:#991b1b}.ico.enr{background:#e0f2fe;color:#075985}.ico.grp{background:#eef2ff;color:#3730a3}.ico.usr{background:#faf5ff;color:#6b21a8}.ico.att{background:#f0fdf4;color:#166534}

  /* Mobile: navbar turns into top bar */
  @media (max-width:900px){
    :root{--nav-w:100vw}
    .side{position:sticky;height:auto;width:100%;left:auto;top:0;border-right:0;border-bottom:1px solid #e5e7eb}
    .nav{display:flex;gap:8px;overflow:auto;padding:10px}
    .nav a{white-space:nowrap}
    .main{margin-left:0}
  }
</style>
</head>
<body>

<!-- Fixed left navbar -->
<aside class="side">
  <div class="brand"><span>EADL</span> Navigation</div>
  <nav class="nav">
    <strong>Overview</strong>
    <a href="./index.html">Home</a>
    <a href="./assets/images/topology.png">Topology image</a>
    <a href="./README.md">Project README</a>
    <hr style="border:none;border-top:1px solid #e5e7eb;margin:10px 6px">
    <strong>Sections</strong>
    <a href="sections/01-ad-baseline.md">01 — AD baseline</a>
    <a href="sections/02-windows-workstation.html">02 — Windows workstation</a>
    <a href="sections/03-linux-workstation.md">03 — Linux workstation</a>
    <a href="sections/04-corporate-server-mailhog.md">04 — Corp server &amp; MailHog</a>
    <a href="sections/05-security-onion-desktop.md">05 — Security Onion desktop</a>
    <a href="sections/06-security-server-sec-box.md">06 — Security server (sec‑box)</a>
    <a href="sections/07-wazuh-manager-install.md">07 — Wazuh manager install</a>
    <a href="sections/08-wazuh-agents-enroll.md">08 — Enroll Wazuh agents</a>
    <a href="sections/09-wazuh-groups-agentconf.md">09 — Wazuh groups &amp; agent.conf</a>
    <a href="sections/10-users-and-snapshots.md">10 — Users &amp; snapshots</a>
    <a href="sections/11-attacker-simulation.md">11 — Attacker &amp; simulation</a>
  </nav>
</aside>

<!-- Main content area -->
<main class="main">
  <div class="hero">
    <div class="strip"></div>
    <div class="hero-body">
      <h1 style="margin:0 0 6px">Enterprise Attack Detection Lab <span style="opacity:.55;font-weight:600">(EADL)</span></h1>
      <p style="margin:6px 0 0;color:#334155">
        Build a realistic mini‑enterprise with AD, Windows/Linux clients, Wazuh XDR, and Security Onion—then attack, detect, and document with verifiable evidence.
      </p>
      <div class="chips">
        <div class="chip">AD domain: <b>corp.eadl-dc.com</b></div>
        <div class="chip">Hosts: <b>6</b></div>
        <div class="chip">Detections: <b>attack &amp; defend</b></div>
      </div>
    </div>
  </div>

  <section class="card">
    <h2 style="margin:0 0 8px">Network topology</h2>
    <p align="center" style="margin:8px 0">
      <img src="./assets/images/topology.png" alt="EADL topology" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px">
    </p>
    <p style="margin:6px 0 0">NAT network with DC, Windows/Linux clients, Wazuh manager, Security Onion, and a corporate server.</p>
  </section>

  <section class="card">
    <h2 style="margin:0 0 8px">Configuration summary</h2>
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
  </section>

  <!-- Showcase overview -->
  <section class="showcase" aria-label="Sections overview">
    <div class="show-head">
      <h2 class="show-title">What’s inside</h2>
      <span style="font-size:12px;color:#475569">High‑level outcomes of each section</span>
    </div>

    <div class="show-grid">
      <div class="sc"><h4><span class="ico ad">AD</span>01 — AD baseline</h4><p>Built a clean Windows Server domain (AD DS, DNS, DHCP) to centralize identity, name resolution, and IP management for all tests.</p><div class="meta"><span class="tag">Windows Server</span><span class="tag">AD DS</span><span class="tag">DNS</span></div></div>
      <div class="sc"><h4><span class="ico win">W</span>02 — Windows workstation</h4><p>Joined Windows 11 to the domain to validate GPO processing, DNS registration, and domain logons under realistic conditions.</p><div class="meta"><span class="tag">GPO</span><span class="tag">Join</span><span class="tag">DNS</span></div></div>
      <div class="sc"><h4><span class="ico linux">L</span>03 — Linux workstation</h4><p>Integrated Ubuntu via Winbind + Kerberos to test cross‑platform identity mapping and ticket‑based SSO.</p><div class="meta"><span class="tag">Winbind</span><span class="tag">Kerberos</span><span class="tag">SSO</span></div></div>
      <div class="sc"><h4><span class="ico mail">M</span>04 — Corp server &amp; MailHog</h4><p>Deployed a safe lab mail stack for phishing and alerting exercises without external SMTP.</p><div class="meta"><span class="tag">SMTP Lab</span><span class="tag">MailHog</span></div></div>
      <div class="sc"><h4><span class="ico so">SO</span>05 — Security Onion desktop</h4><p>Explored Zeek/Suricata telemetry and practiced packet‑driven triage workflows.</p><div class="meta"><span class="tag">Zeek</span><span class="tag">Suricata</span><span class="tag">NSM</span></div></div>
      <div class="sc"><h4><span class="ico sec">S</span>06 — Security server (sec‑box)</h4><p>Hardened the monitoring host, expanded disk, and prepared for SIEM tools.</p><div class="meta"><span class="tag">Hardening</span><span class="tag">Storage</span></div></div>
      <div class="sc"><h4><span class="ico wz">WZ</span>07 — Wazuh manager install</h4><p>Installed Wazuh (indexer + dashboard) to centralize endpoint telemetry and detections.</p><div class="meta"><span class="tag">Wazuh</span><span class="tag">Indexer</span><span class="tag">Dashboard</span></div></div>
      <div class="sc"><h4><span class="ico enr">E</span>08 — Enroll Wazuh agents</h4><p>Onboarded Windows/Linux endpoints and verified heartbeats, logs, and baseline rules.</p><div class="meta"><span class="tag">Windows</span><span class="tag">Linux</span><span class="tag">Agents</span></div></div>
      <div class="sc"><h4><span class="ico grp">G</span>09 — Groups &amp; agent.conf</h4><p>Pushed FIM, Sysmon, and auditd via groups to standardize detections at scale.</p><div class="meta"><span class="tag">FIM</span><span class="tag">Sysmon</span><span class="tag">auditd</span></div></div>
      <div class="sc"><h4><span class="ico usr">U</span>10 — Users &amp; snapshots</h4><p>Created users, mapped shares, and captured golden snapshots for repeatable labs.</p><div class="meta"><span class="tag">Users</span><span class="tag">Shares</span><span class="tag">Snapshots</span></div></div>
      <div class="sc"><h4><span class="ico att">A</span>11 — Attacker &amp; simulation</h4><p>Executed controlled techniques to validate detections end‑to‑end and document evidence.</p><div class="meta"><span class="tag">ATT&amp;CK</span><span class="tag">Detections</span></div></div>
    </div>
  </section>

  <div style="height:32px"></div>
</main>

</body>
</html>
