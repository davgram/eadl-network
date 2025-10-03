---
title: Security server (sec-box) prep
nav_order: 6
---

[← Back to index](../index.md){: .btn .btn-blue }

# Security server (sec-box) prep

<!-- Intro callout -->
<div style="
  border:1px solid #e5e7eb;
  border-left:6px solid #2563eb;
  background:#f8fafc;
  padding:14px 16px;
  border-radius:8px;
  margin:12px 0 18px 0;
">
  <div style="display:flex;align-items:flex-start;gap:10px;">
    <div style="font-size:22px;line-height:1;">🛡️</div>
    <div>
      <p style="margin:0 0 6px 0;font-weight:600;">Goal</p>
      <p style="margin:0;">
        Clone the Linux workstation into <code>sec-box</code>, create a local admin, set a static IP, join the AD domain,
        verify Winbind, and snapshot the VM before installing Wazuh.
      </p>
    </div>
  </div>
</div>

## 1) Clone the Linux machine

- VirtualBox → select Linux workstation → Right‑click → Clone → Full clone → include snapshots → Finish.  
- Power on the clone.

## 2) Rename hostname

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>sudo nano /etc/hostname</code></pre>

Replace contents with:

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>sec-box</code></pre>

Then reboot:

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>sudo reboot</code></pre>

## 3) Create local admin and grant sudo

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>cd ..
sudo adduser sec-user</code></pre>

<img src="../assets/images/06-security-server-sec-box/page.png" alt="adduser sec-user prompt" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

Grant and test:

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>sudo usermod -aG sudo sec-user
sudo su - sec-user
whoami</code></pre>

<img src="../assets/images/06-security-server-sec-box/whoami.png" alt="whoami shows sec-user" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

## 4) Network settings (static IP)

- Top bar → Wired connected → Wired Settings → gear icon → IPv4 → Manual → apply settings as shown.

<img src="../assets/images/06-security-server-sec-box/ipstatic.png" alt="IPv4 static configuration" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

Test DC reachability:

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>ping -c 3 eadl-dc</code></pre>

<img src="../assets/images/06-security-server-sec-box/ping.png" alt="Ping DC successful" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

## 5) Create the domain user (on DC)

- DC → Tools → Active Directory Users and Computers → Users → Right‑click → New → User → finish wizard.

<img src="../assets/images/06-security-server-sec-box/adduser.png" alt="Create new AD user" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

- Right‑click user → Properties → Member Of → confirm Domain Users.

<img src="../assets/images/06-security-server-sec-box/admingroup.png" alt="Member Of shows Domain Users" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

Optional group management:

<div style="display:flex;gap:10px;flex-wrap:wrap;">
  <img src="../assets/images/06-security-server-sec-box/admingroup2.png" alt="Create admin group" width="360" style="max-width:49%;min-width:260px;border:1px solid #e5e7eb;border-radius:6px;">
  <img src="../assets/images/06-security-server-sec-box/domainuser.png" alt="Add Domain Users to group" width="360" style="max-width:49%;min-width:260px;border:1px solid #e5e7eb;border-radius:6px;">
</div>

## 6) Join sec-box to the domain

Ensure DNS points to the DC and the clock is in sync.

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>sudo systemctl restart winbind
sudo net ads join -U Administrator
sudo systemctl restart winbind</code></pre>

Verify:

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>wbinfo -u | head</code></pre>

<img src="../assets/images/06-security-server-sec-box/wbinfo.png" alt="wbinfo -u output" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

Login test (create home):

<pre style="background:#0b1021;color:#e5e7eb;padding:12px;border-radius:6px;overflow:auto;"><code>sudo login</code></pre>

<img src="../assets/images/06-security-server-sec-box/dir.png" alt="Home directory created for domain user" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">

## 7) Snapshot before Wazuh

- Create snapshot “pre‑wazuh”.

<img src="../assets/images/06-security-server-sec-box/snapshot.png" alt="Snapshot pre-wazuh created" width="720" style="max-width:100%;border:1px solid #e5e7eb;border-radius:6px;">
