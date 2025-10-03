---
title: Security server (sec-box) prep
nav_order: 6
---

[← Back to index](../index.md){: .btn .btn-blue }

# Security server (sec-box) prep

<!-- Intro callout -->
<div style="
  border:1px solid #e5e7eb;
  border-left:6px solid #16a34a;
  background:#f0fdf4;
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

## 1) Clone the VM

- VirtualBox → select the Linux workstation → Right‑click → Clone → Full clone → include snapshots → Finish.  
- Power on the clone.

## 2) Rename hostname

