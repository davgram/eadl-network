<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>EADL — Enterprise Attack Detection Lab</title>
<style>
  html{scroll-behavior:smooth}
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
  .brand{padding:14px 14px 12px;border-bottom:1px solid #e5e7eb;font-weight:800}
  .brand span{background:linear-gradient(90deg,#38bdf8,#22c55e,#a78bfa);-webkit-background-clip:text;background-clip:text;color:transparent}
  .nav{padding:12px}
  .nav strong{display:block;margin:0 6px 8px 6px}
  .nav button{
    display:block;width:100%;text-align:left;cursor:pointer;
    margin:8px 6px;padding:8px 10px;border:1px solid #e5e7eb;border-radius:8px;background:#fff;color:#0f172a;
    font:inherit;
  }
  .nav button:hover{background:#f1f5f9}

  /* Content blocks */
  .hero{border:1px solid #e5e7eb;border-radius:12px;overflow:hidden;margin:8px 0 18px;box-shadow:0 3px 16px rgba(2,6,23,.06)}
  .strip{height:6px;background:linear-gradient(90deg,#0ea5e9,#22c55e,#a855f7)}
  .hero-body{padding:16px}
  .chips{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
  .chip{border:1px solid #e5e7eb;background:#fff;padding:6px 10px;border-radius:999px;font-size:12px}
  .card{border:1px solid #e5e7eb;border-radius:10px;padding:14px;margin:10px 0 16px;background:#fff}
  table{border-collapse:collapse;width:100%;font-size:14px}
  th,td{padding:8px 6px;border-bottom:1px solid #eaeef3;text-align:left}

  /* Anchor targets: ensure they are focusable and offset-safe */
  section{scroll-margin-top:14px}
  section[tabindex="-1"]{outline:0}
</style>
</head>
<body>

<div class="wrap">
  <!-- Left navbar (buttons to avoid <a> sanitization) -->
  <aside class="side">
    <div class="brand"><span>EADL</span> Navigation</div>
    <nav class="nav" id="left-nav">
      <strong>Overview</strong>
      <button type="button" data-target="intro">Intro</button>
      <button type="button" data-target="topology">Topology</button>
      <button type="button" data-target="config">Configuration</button>
      <button type="button" data-target="evidence">Evidence</button>
      <hr style="border:none;border-top:1px solid #e5e7eb;margin:10px 6px">

      <strong>Sections</strong>
      <button type="button" data-target="s01">01 — AD baseline</button>
      <button type="button" data-target="s02">02 — Windows workstation</button>
      <button type="button" data-target="s03">03 — Linux workstation</button>
      <button type="button" data-target="s04">04 — Corp server &amp; MailHog</button>
      <button type="button" data-target="s05">05 — Security Onion desktop</button>
      <button type="button" data-target="s06">06 — Security server (sec‑box)</button>
      <button type="button" data-target="s07">07 — Wazuh manager</button>
      <button type="button" data-target="s08">08 — Enroll agents</button>
      <button type="button" data-target="s09">09 — Groups &amp; agent.conf</button>
      <button type="button" data-target="s10">10 — Users &amp; snapshots</button>
      <button type="button" data-target="s11">11 — Attacker &amp; simulation</button>
    </nav>
  </aside>

  <!-- Content -->
  <main class="main" id="content">
    <!-- Intro -->
    <section id="intro" tabindex="-1" class="hero">
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
    </section>

    <!-- Topology -->
    <section id="topology" tabindex="-1" class="card">
      <h2 style="margin:0 0 8px">Topology</h2>
      <p align="center" style="margin:8px 0">
        <img src="./assets/images/topology.png" alt="EADL topology" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px">
      </p>
      <p style="margin:6px 0 0">NAT network with DC, Windows/Linux clients, Wazuh manager, Security Onion, and a corporate server.</p>
    </section>

    <!-- Configuration -->
    <section id="config" tabindex="-1">
      <div class="card">
        <h2 style="margin:0 0 8px">Configuration summary</h2>
        <h3 style="margin:10px 0 6px">Hosts</h3>
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
        <h3 style="margin:0 0 6px">VM specs</h3>
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
        <h3 style="margin:0 0 6px">Core network</h3>
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
        <h3 style="margin:0 0 6px">Accounts (public‑safe placeholders)</h3>
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
    <section id="evidence" tabindex="-1" class="card">
      <h2 style="margin:0 0 8px">Evidence gallery</h2>
      <ul style="margin:0 0 10px 16px">
        <li>Domain join (Windows): <img src="./assets/images/win-join.png" alt="Windows domain join success" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
        <li>Domain join (Linux): <img src="./assets/images/linux-join.png" alt="Linux domain join success via Winbind" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
        <li>Wazuh manager dashboard: <img src="./assets/images/wazuh-ui.png" alt="Wazuh dashboard" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
        <li>Security Onion desktop: <img src="./assets/images/so-desktop.png" alt="Security Onion desktop" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
        <li>MailHog UI: <img src="./assets/images/mailhog-ui.png" alt="MailHog web UI" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px"></li>
      </ul>
    </section>

    <!-- Section anchors -->
    <section id="s01" tabindex="-1" class="card"><h3 style="margin:0 0 6px">01 — Active Directory baseline</h3><p style="margin:0">Install Windows Server, configure AD DS/DNS/DHCP, and prepare the lab domain.</p></section>
    <section id="s02" tabindex="-1" class="card"><h3 style="margin:0 0 6px">02 — Windows workstation</h3><p style="margin:0">Join Windows 11 to the domain and verify GPO, DNS, and logon.</p></section>
    <section id="s03" tabindex="-1" class="card"><h3 style="margin:0 0 6px">03 — Linux workstation</h3><p style="margin:0">Join Ubuntu via Winbind + Kerberos; test domain logins and id mapping.</p></section>
    <section id="s04" tabindex="-1" class="card"><h3 style="margin:0 0 6px">04 — Corporate server &amp; MailHog</h3><p style="margin:0">Deploy lab mail stack for phishing and alerting exercises.</p></section>
    <section id="s05" tabindex="-1" class="card"><h3 style="margin:0 0 6px">05 — Security Onion desktop</h3><p style="margin:0">Use analyst workstation to explore Zeek/Suricata logs and detections.</p></section>
    <section id="s06" tabindex="-1" class="card"><h3 style="margin:0 0 6px">06 — Security server (sec‑box) prep</h3><p style="margin:0">Harden Ubuntu base, expand disk, and prepare for Wazuh.</p></section>
    <section id="s07" tabindex="-1" class="card"><h3 style="margin:0 0 6px">07 — Wazuh manager install</h3><p style="margin:0">Install Wazuh, configure indexer and dashboard, validate health.</p></section>
    <section id="s08" tabindex="-1" class="card"><h3 style="margin:0 0 6px">08 — Enroll Wazuh agents</h3><p style="margin:0">Enroll Windows/Linux agents and verify connectivity and logs.</p></section>
    <section id="s09" tabindex="-1" class="card"><h3 style="margin:0 0 6px">09 — Wazuh groups &amp; agent.conf</h3><p style="margin:0">Create Windows/Linux groups; push FIM, Sysmon, and auditd configs.</p></section>
    <section id="s10" tabindex="-1" class="card"><h3 style="margin:0 0 6px">10 — Users, mapping &amp; snapshots</h3><p style="margin:0">Create domain users, map shares, and snapshot golden states.</p></section>
    <section id="s11" tabindex="-1" class="card"><h3 style="margin:0 0 6px">11 — Optional: Attacker &amp; simulation</h3><p style="margin:0">Run controlled attacks and validate detection coverage.</p></section>

    <div style="height:28px"></div>
  </main>
</div>

<script>
  // Robust navigation handler using data-target and focusable anchors.
  document.addEventListener('DOMContentLoaded', function(){
    var nav = document.getElementById('left-nav');
    if(!nav) return;
    nav.addEventListener('click', function(e){
      if(e.target.tagName !== 'BUTTON') return;
      var id = e.target.getAttribute('data-target');
      var el = document.getElementById(id);
      if(!el) return;
      // Focus the section (works even in sandboxed renderers), then smooth scroll.
      el.focus({preventScroll:true});
      el.scrollIntoView({behavior:'smooth', block:'start'});
      try { history.replaceState(null,'','#'+id); } catch(_) {}
    });
  });
</script>

</body>
</html>
