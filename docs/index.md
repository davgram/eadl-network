<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>EADL — Enterprise Attack Detection Lab</title>
<style>
  body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Arial;color:#0f172a;background:#ffffff}
  a{color:#2563eb;text-decoration:none}
  /* Layout */
  .wrap{display:flex;min-height:100vh}
  .side{
    position:sticky;top:0;align-self:flex-start;
    width:240px;min-width:240px;max-height:100vh;overflow:auto;
    border-right:1px solid #e5e7eb;background:linear-gradient(180deg,#f8fafc,#fff);
  }
  .main{flex:1;min-width:0;padding:16px 18px}
  @media (max-width:900px){
    .wrap{flex-direction:column}
    .side{position:static;width:auto;min-width:0;max-height:none;border-right:0;border-bottom:1px solid #e5e7eb}
  }
  /* Sidebar */
  .brand{padding:14px;border-bottom:1px solid #e5e7eb;font-weight:800}
  .brand span{background:linear-gradient(90deg,#38bdf8,#22c55e,#a78bfa);-webkit-background-clip:text;background-clip:text;color:transparent}
  .nav{padding:12px}
  .nav strong{display:block;margin:0 6px 8px}
  .nav a{display:block;margin:8px 6px;padding:8px 10px;border:1px solid #e5e7eb;border-radius:8px;background:#fff;color:#0f172a}
  .nav a:hover{background:#f1f5f9}
  /* Content */
  .hero{border:1px solid #e5e7eb;border-radius:12px;overflow:hidden;margin:8px 0 18px;box-shadow:0 3px 16px rgba(2,6,23,.06)}
  .strip{height:6px;background:linear-gradient(90deg,#0ea5e9,#22c55e,#a855f7)}
  .hero-body{padding:16px}
  .chips{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
  .chip{border:1px solid #e5e7eb;background:#fff;padding:6px 10px;border-radius:999px;font-size:12px}
  .card{border:1px solid #e5e7eb;border-radius:10px;padding:14px;margin:10px 0 16px;background:#fff}
  table{border-collapse:collapse;width:100%;font-size:14px}
  th,td{padding:8px 6px;border-bottom:1px solid #eaeef3;text-align:left}
</style>
</head>
<body>

<div class="wrap">
  <!-- Left navbar: ONLY navigation to separate pages -->
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

  <!-- Main page: hero + topology + compact config only -->
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

    <div style="height:32px"></div>
  </main>
</div>

</body>
</html>
