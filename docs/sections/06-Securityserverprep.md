---
title: Linux workstation (AD join)
nav_order: 3
---

[← Back to index](../index.md){: .btn .btn-blue }


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>06 — Security server (sec-box) prep</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
  body { font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif; color:#0f172a; line-height:1.55; }
  .container { max-width: 920px; margin: 0 auto; padding: 16px; }
  a.btn { display:inline-block; padding:8px 12px; border:1px solid #e5e7eb; border-radius:6px; text-decoration:none; background:#eff6ff; color:#1d4ed8; }
  h1 { font-size: 28px; margin: 12px 0 8px; }
  h2 { font-size: 20px; margin: 20px 0 10px; }
  pre { background:#0b1021; color:#e5e7eb; padding:12px; border-radius:6px; overflow:auto; }
  code { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; }
  .card { border:1px solid #e5e7eb; border-radius:8px; padding:14px; background:#fff; }
  .img { max-width:100%; border:1px solid #e5e7eb; border-radius:6px; }
  hr { border:0; border-top:1px solid #e5e7eb; margin:18px 0; }
  ul { margin: 0 0 10px 18px; }
</style>
</head>
<body>
<div class="container">

<p><a class="btn" href="../index.md">← Back to index</a></p>

<h1>Security server (sec-box) prep</h1>

<div class="card">
  <p>This page clones the Linux workstation, renames it to <b>sec-box</b>, creates a local admin, sets a static IP, joins the AD domain, verifies Winbind, and snapshots the VM before installing Wazuh.</p>
  <p>Screenshots path: <code>docs/assets/sec-boxprep</code>.</p>
</div>

<hr>

<h2>1) Clone the Linux VM</h2>
<ul>
  <li>VirtualBox → select the Linux workstation → Right‑click → Clone → Full clone → include snapshots → Finish.</li>
  <li>Power on the clone.</li>
</ul>

<h2>2) Rename hostname</h2>
<pre><code>sudo nano /etc/hostname
</code></pre>
<p>Replace contents with:</p>
<pre><code>sec-box
</code></pre>
<p>Save and reboot:</p>
<pre><code>sudo reboot
</code></pre>

<h2>3) Create a local admin and grant sudo</h2>
<p>Create the user and set the password:</p>
<pre><code>cd ..
sudo adduser sec-user
</code></pre>
<p><img class="img" src="../assets/sec-boxprep/page.png" alt="adduser sec-user prompt"></p>

<p>Grant sudo privileges and verify:</p>
<pre><code>sudo usermod -aG sudo sec-user
sudo su - sec-user
whoami
</code></pre>
<p><img class="img" src="../assets/sec-boxprep/whoami.png" alt="whoami shows sec-user"></p>

<h2>4) Configure static IP</h2>
<p>Top bar → Wired connected → Wired Settings → gear icon → IPv4 → Manual → apply settings as in the screenshot.</p>
<p><img class="img" src="../assets/sec-boxprep/ipstatic.png" alt="IPv4 static configuration"></p>

<p>Test connection to the domain controller:</p>
<pre><code>ping -c 3 eadl-dc
</code></pre>
<p><img class="img" src="../assets/sec-boxprep/ping.png" alt="Ping DC successful"></p>

<h2>5) Create the domain user on the DC</h2>
<ul>
  <li>On the domain controller: Tools → Active Directory Users and Computers → Users → Right‑click → New → User.</li>
</ul>
<p><img class="img" src="../assets/sec-boxprep/adduser.png" alt="Create new AD user wizard"></p>

<p>Open the user → Member Of → verify Domain Users.</p>
<p><img class="img" src="../assets/sec-boxprep/admingroup.png" alt="Member Of shows Domain Users"></p>

<p>Optional: create an admin group and assign members.</p>
<p><img class="img" src="../assets/sec-boxprep/admingroup2.png" alt="Create admin group"></p>
<p><img class="img" src="../assets/sec-boxprep/domainuser.png" alt="Add Domain Users to group"></p>

<h2>6) Join sec-box to the domain</h2>
<p>Ensure DNS points to the DC and time is in sync.</p>
<pre><code>sudo systemctl restart winbind
sudo net ads join -U Administrator
sudo systemctl restart winbind
</code></pre>

<p>Verify domain users:</p>
<pre><code>wbinfo -u | head
</code></pre>
<p><img class="img" src="../assets/sec-boxprep/wbinfo.png" alt="wbinfo -u shows domain users"></p>

<h2>7) Test login and directory creation</h2>
<p>Login via terminal:</p>
<pre><code>sudo login
</code></pre>
<p>A home directory for the domain account should be created automatically.</p>
<p><img class="img" src="../assets/sec-boxprep/dir.png" alt="Home directory created"></p>

<h2>8) Take a snapshot before Wazuh installation</h2>
<p>Create a VM snapshot named “pre‑wazuh”.</p>
<p><img class="img" src="../assets/sec-boxprep/snapshot.png" alt="Snapshot pre-wazuh created"></p>

<hr>

<h2>Next steps</h2>
<p>Proceed with the Wazuh installation on <b>sec-box</b>.</p>

</div>
</body>
</html>
