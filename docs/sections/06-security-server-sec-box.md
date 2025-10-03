---
title: Security server (sec-box) prep
nav_order: 6
---

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>06 — Security server (sec-box) prep</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
  :root{
    --border:#e5e7eb;
    --ink:#0b1220;
    --muted:#334155;
    --bg:#ffffff;
    --callout:#f0fdf4;
    --callout-border:#16a34a;
    --code-bg:#0f172a;
    --code-fg:#e2e8f0;
    --code-accent:#60a5fa;
  }
  html,body{margin:0;padding:0;background:var(--bg);color:var(--ink);font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;line-height:1.6}
  .container{max-width:980px;margin:0 auto;padding:18px}
  a.btn{display:inline-block;text-decoration:none;border:1px solid var(--border);padding:8px 12px;border-radius:8px;background:#eff6ff;color:#1d4ed8}
  h1{font-size:28px;margin:12px 0 6px}
  h2{font-size:22px;margin:22px 0 10px}
  p{margin:10px 0}
  ul{margin:6px 0 12px 22px}
  li{margin:4px 0}
  hr{border:0;border-top:1px solid var(--border);margin:22px 0}
  .callout{border:1px solid var(--border);border-left:6px solid var(--callout-border);background:var(--callout);padding:14px 16px;border-radius:8px;margin:12px 0 18px 0}
  pre{background:var(--code-bg);color:var(--code-fg);padding:14px;border-radius:8px;overflow:auto;margin:10px 0 14px 0;box-shadow:inset 0 0 0 1px rgba(255,255,255,.04)}
  code,kbd{font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,Monaco,monospace;font-size:14px}
  kbd{border:1px solid var(--border);border-bottom-width:2px;padding:2px 6px;border-radius:6px;background:#f8fafc}
  .img{max-width:100%;border:1px solid var(--border);border-radius:8px}
  .pair{display:flex;gap:10px;flex-wrap:wrap}
  .pair img{max-width:49%;min-width:260px}
  .code-title{color:#93c5fd;font-weight:700;margin:4px 0 4px 0;font-size:13px;letter-spacing:.2px}
</style>
</head>
<body>
<div class="container">

<p><a class="btn" href="../index.md">← Back to index</a></p>

<h1>Security server (sec-box) prep</h1>

<div class="callout">
  Clone the Linux workstation into <b>sec-box</b>, create a local admin, set a static IP, join the AD domain, verify Winbind, and snapshot the VM before installing Wazuh. Screenshots: <code>/assets/images/06-security-server-sec-box</code>.
</div>

<hr>

<h2>1) Clone the Linux machine</h2>
<ul>
  <li>VirtualBox → select Linux workstation → Right‑click → Clone → <b>Full clone</b> → include snapshots → Finish.</li>
  <li>Power on the clone.</li>
</ul>

<h2>2) Rename hostname</h2>
<div class="code-title">Command</div>
<pre><code>sudo nano /etc/hostname</code></pre>
<p>Replace with:</p>
<div class="code-title">New value</div>
<pre><code>sec-box</code></pre>
<p>Then reboot:</p>
<div class="code-title">Reboot</div>
<pre><code>sudo reboot</code></pre>

<h2>3) Create local admin and grant sudo</h2>
<div class="code-title">Create account</div>
<pre><code>cd ..
sudo adduser sec-user</code></pre>
<p><img class="img" src="../assets/images/06-security-server-sec-box/page.png" alt="adduser sec-user prompt"></p>

<div class="code-title">Grant sudo and verify</div>
<pre><code>sudo usermod -aG sudo sec-user
sudo su - sec-user
whoami</code></pre>
<p><img class="img" src="../assets/images/06-security-server-sec-box/whoami.png" alt="whoami shows sec-user"></p>

<h2>4) Network settings (static IP)</h2>
<p>Top bar → Wired connected → Wired Settings → gear icon → IPv4 → Manual → configure as in the screenshot.</p>
<p><img class="img" src="../assets/images/06-security-server-sec-box/ipstatic.png" alt="IPv4 static configuration"></p>

<div class="code-title">Test DC reachability</div>
<pre><code>ping -c 3 eadl-dc</code></pre>
<p><img class="img" src="../assets/images/06-security-server-sec-box/ping.png" alt="Ping DC successful"></p>

<h2>5) Create the domain user (on DC)</h2>
<ul>
  <li>DC → Tools → Active Directory Users and Computers → Users → Right‑click → New → User → finish wizard.</li>
</ul>
<p><img class="img" src="../assets/images/06-security-server-sec-box/adduser.png" alt="Create new AD user"></p>

<p>Open the user → <b>Member Of</b> → verify <b>Domain Users</b>.</p>
<p><img class="img" src="../assets/images/06-security-server-sec-box/admingroup.png" alt="Member Of shows Domain Users"></p>

<p>(Optional) Create an admin group and assign members.</p>
<div class="pair">
  <img class="img" src="../assets/images/06-security-server-sec-box/admingroup2.png" alt="Create admin group">
  <img class="img" src="../assets/images/06-security-server-sec-box/domainuser.png" alt="Add Domain Users to group">
</div>

<h2>6) Join sec-box to the domain</h2>
<p>Ensure DNS points to the DC and the clock is in sync.</p>
<div class="code-title">Join sequence</div>
<pre><code>sudo systemctl restart winbind
sudo net ads join -U Administrator
sudo systemctl restart winbind</code></pre>

<div class="code-title">Verify enumeration</div>
<pre><code>wbinfo -u | head</code></pre>
<p><img class="img" src="../assets/images/06-security-server-sec-box/wbinfo.png" alt="wbinfo -u output"></p>

<h2>7) First domain login (home created)</h2>
<div class="code-title">Login</div>
<pre><code>sudo login</code></pre>
<p>After first domain login a home directory is created automatically.</p>
<p><img class="img" src="../assets/images/06-security-server-sec-box/dir.png" alt="Home directory created for domain user"></p>

<h2>8) Snapshot before Wazuh</h2>
<p>Create a VM snapshot named <b>pre‑wazuh</b> in VirtualBox.</p>
<p><img class="img" src="../assets/images/06-security-server-sec-box/snapshot.png" alt="Snapshot pre-wazuh created"></p>

</div>
</body>
</html>
