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
    --ink:#0f172a;
    --muted:#334155;
    --bg:#ffffff;
    --callout:#f0fdf4;
    --callout-border:#16a34a;
    --code-bg:#0b1021;
    --code-fg:#e5e7eb;
  }
  html,body{margin:0;padding:0;background:#fff;color:var(--ink);font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;line-height:1.55}
  .container{max-width:980px;margin:0 auto;padding:18px}
  a.btn{display:inline-block;text-decoration:none;border:1px solid var(--border);padding:8px 12px;border-radius:8px;background:#eff6ff;color:#1d4ed8}
  h1{font-size:28px;margin:12px 0 6px}
  h2{font-size:20px;margin:18px 0 8px}
  p{margin:8px 0}
  ul{margin:6px 0 12px 20px}
  hr{border:0;border-top:1px solid var(--border);margin:18px 0}
  .callout{border:1px solid var(--border);border-left:6px solid var(--callout-border);background:var(--callout);padding:14px 16px;border-radius:8px;margin:12px 0 18px 0}
  pre{background:var(--code-bg);color:var(--code-fg);padding:12px;border-radius:6px;overflow:auto}
  code{font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace}
  .img{max-width:100%;border:1px solid var(--border);border-radius:6px}
  .pair{display:flex;gap:10px;flex-wrap:wrap}
  .pair img{max-width:49%;min-width:260px}
</style>
</head>
<body>
<div class="container">

<p><a class="btn" href="../index.md">← Back to index</a></p>

<h1>Security server (sec-box) prep</h1>

<div class="callout">
  This page follows the same structure as the Linux workstation (03) page but for <b>sec-box</b>: clone the VM, rename host, create a local admin, set a static IP, join the AD domain, verify Winbind, and snapshot before Wazuh.
</div>

<hr>

<h2>1) Clone the Linux Machine</h2>
<ul>
  <li>VirtualBox → select Linux workstation → Right‑click → Clone → <b>Full clone</b> → include snapshots → Finish.</li>
  <li>Power on the clone.</li>
</ul>

<h2>2) Rename hostname</h2>
<pre><code>sudo nano /etc/hostname
</code></pre>
<p>Replace the current value with:</p>
<pre><code>sec-box
</code></pre>
<p>Then reboot:</p>
<pre><code>sudo reboot
</code></pre>

<h2>3) Create local admin and grant sudo</h2>
<p>Create the account and set the password:</p>
<pre><code>cd ..
sudo adduser sec-user
</code></pre>
<p><img class="img" src="../assets/sec-boxprep/page.png" alt="adduser sec-user prompt"></p>

<p>Grant sudo and verify:</p>
<pre><code>sudo usermod -aG sudo sec-user
sudo su - sec-user
whoami
</code></pre>
<p><img class="img" src="../assets/sec-boxprep/whoami.png" alt="whoami shows sec-user"></p>

<h2>4) Network settings (static IP)</h2>
<p>Top nav → Wired connected → Wired Settings → gear icon → IPv4 → Manual → configure as shown.</p>
<p><img class="img" src="../assets/sec-boxprep/ipstatic.png" alt="IPv4 static configuration"></p>

<p>Confirm connectivity to the domain controller:</p>
<pre><code>ping -c 3 eadl-dc
</code></pre>
<p><img class="img" src="../assets/sec-boxprep/ping.png" alt="Ping DC successful"></p>

<h2>5) Create the domain user on the DC</h2>
<ul>
  <li>On the DC: Tools → Active Directory Users and Computers → Users → Right‑click → New → User → finish wizard.</li>
</ul>
<p><img class="img" src="../assets/sec-boxprep/adduser.png" alt="Create new AD user wizard"></p>

<p>Right‑click the user → Properties → <b>Member Of</b> → verify <b>Domain Users</b>.</p>
<p><img class="img" src="../assets/sec-boxprep/admingroup.png" alt="Member Of shows Domain Users"></p>

<p>(Optional) Create an admin group and assign users:</p>
<div class="pair">
  <img class="img" src="../assets/sec-boxprep/admingroup2.png" alt="Create admin group">
  <img class="img" src="../assets/sec-boxprep/domainuser.png" alt="Add Domain Users to group">
</div>

<h2>6) Join sec-box to the domain</h2>
<p>Ensure DNS points to the DC and system time matches the DC.</p>
<pre><code>sudo systemctl restart winbind
sudo net ads join -U Administrator
sudo systemctl restart winbind
</code></pre>

<p>Verify enumeration:</p>
<pre><code>wbinfo -u | head
</code></pre>
<p><img class="img" src="../assets/sec-boxprep/wbinfo.png" alt="wbinfo -u output"></p>

<h2>7) First domain login (home created)</h2>
<pre><code>sudo login
</code></pre>
<p>After login, the domain user’s home directory is created automatically.</p>
<p><img class="img" src="../assets/sec-boxprep/dir.png" alt="Home directory created for domain user"></p>

<h2>8) Snapshot before Wazuh installation</h2>
<p>Create a VM snapshot named <b>pre‑wazuh</b> in VirtualBox.</p>
<p><img class="img" src="../assets/sec-boxprep/snapshot.png" alt="Snapshot pre-wazuh created"></p>

<hr>

<h2>Troubleshooting (Jekyll/Pages)</h2>
<ul>
  <li>Front matter must be the first lines in the file with exact <code>---</code> delimiters (no spaces or BOM).</li>
  <li>Leave blank lines before and after HTML blocks so Kramdown doesn’t treat following Markdown as raw text.</li>
  <li>If embedding complex HTML inside Markdown, add <code>markdown="1"</code> on the container to force parsing.</li>
  <li>Button classes like <code>{: .btn .btn-blue }</code> only apply if the page renders without earlier markup errors.</li>
</ul>

</div>
</body>
</html>
