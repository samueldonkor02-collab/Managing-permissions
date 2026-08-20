# Managing-permissions
Hands on Windows &amp; Linux file permissions lab — part of my journey from healthcare into cybersecurity.
# 🔐 Who Gets the Keys? A Hands-On Lab in Windows & Linux File Permissions

*From patient charts to permission charts — my journey from healthcare to cybersecurity, one lab at a time.*

---

## 👋 About Me

I spent years in healthcare learning something that turns out to be the entire foundation of cybersecurity: **not everyone should have access to everything.** HIPAA taught me the *why* behind least privilege long before I knew the term for it. Now I'm channeling that instinct into a career in cybersecurity — and this repo is where I document the hands-on labs that are getting me there.

If you're a hiring manager, recruiter, or fellow career-changer: welcome. This is one of the first stops on my path from clinical access controls to enterprise access controls.

---

## 🎯 Project Overview

This lab focuses on **file and folder permissions management** across both **Windows** and **Linux** environments — a core skill for any entry-level security or sysadmin role. Misconfigured permissions are one of the most common (and most preventable) causes of data breaches, so understanding how to read, set, and audit them is non-negotiable in this field.

**Environment:** Windows 10 (PC10, domain `structureality.com`) + Kali Linux, via a cloud-based lab platform (LabOnDemand).

---

## 🛠️ What I Practiced

### 🪟 Windows — NTFS & Share Permissions
- Explored **NTFS permissions** via `LABFILES Properties → Security → Advanced` on `C:\LABFILES`
- Reviewed default ACL entries: `Everyone`, `SYSTEM`, `Administrators`, `Users`, `CREATOR OWNER`
- Used the **Effective Access** tool to check exactly what a specific user (`dylan@structureality.com`) could and couldn't do on a resource — a great way to troubleshoot "why can't this user open the file?" tickets
- Managed permissions from the command line with **`icacls`**:
  ```powershell
  icacls .\comptia-logo.jpg /deny dylan:R
  icacls .\comptia-logo.jpg /grant dylan:F
  icacls .\comptia-logo.jpg /remove:g dylan
  ```
- Created and managed a **network share** with PowerShell's SMB cmdlets:
  ```powershell
  New-SmbShare -Name "LABFILES" -Path "C:\LABFILES" -Description "Share for LABFILES"
  Get-SmbShareAccess -Name "LABFILES"
  Grant-SmbShareAccess -Name "LABFILES" -AccountName "dylan" -AccessRight Change
  Revoke-SmbShareAccess -Name "LABFILES" -AccountName "dylan"
  ```
- Learned firsthand that **share permissions and NTFS permissions stack** — the more restrictive of the two always wins. This distinction trips up a lot of newcomers (it tripped me up too, at first).

### 🐧 Linux — chmod & File Modes
- Practiced reading and modifying permissions with `ls -l` and `chmod` in Kali Linux:
  ```bash
  chmod u+x testfile.txt      # -rwxr--r--
  chmod g+w testfile.txt      # -rwxrw-r--
  chmod 777 testfile.txt      # -rwxrwxrwx
  chmod 740 testfile.txt      # -rwxr-----
  chmod 654 testfile.txt      # -rw-r-xr--
  ```
- Built muscle memory translating between **symbolic** (`u+x`, `g+w`) and **numeric/octal** (`777`, `740`, `654`) permission notation — a must-have skill for any Linux-adjacent security role.

---

## 🧠 Skills Demonstrated

| Category | Skills |
|---|---|
| **Windows Administration** | NTFS ACLs, Advanced Security Settings, Effective Access analysis, `icacls` |
| **Windows Networking** | SMB share creation & access control (PowerShell) |
| **Linux Administration** | `chmod`, symbolic vs. octal permissions, file mode auditing |
| **Security Concepts** | Principle of least privilege, allow vs. deny, permission inheritance, access troubleshooting |
| **Tools** | Windows PowerShell, Kali Linux terminal, File Explorer Security tab |

---

## 📝 What I Learned

This was an assisted lab, so I want to be upfront about where my understanding actually is right now — I'd rather be honest here than overstate it and get caught out in an interview.

- **The principle of least privilege clicked for me here.** Watching access get granted to `dylan` and then deliberately revoked afterward made it obvious *why* you don't leave permissions sitting around once they're not needed anymore — every unused access point is just risk with no upside.
- **Deny overrides Allow.** This was the clearest technical takeaway for me: even with broader access granted elsewhere, a single deny rule blocks that action. It's a simple rule, but it explains a lot of "why can't this user do X" situations.
- **Access should be intentional, not default.** Seeing how many permission entries exist by default (Everyone, Users, SYSTEM, etc.) made me think about how easy it is for access to be broader than it needs to be if nobody's paying attention.

I'm still building my depth on the mechanics — things like how NTFS and share permissions interact, or the full logic behind `icacls` syntax — and that's exactly why I'm doing labs like this one and writing them up. I'd rather be honest about being early in this than pretend I've mastered it after one guided walkthrough.

---

## 💡 Why This Matters

Every healthcare system I ever touched had role-based access controls deciding who could see what. Cybersecurity runs on the exact same logic — just applied to files, shares, systems, and networks instead of medical records. Learning to configure, audit, and troubleshoot permissions is one of the most practical, immediately-useful skills for an entry-level SOC analyst, help desk, or sysadmin role, and this lab was my first deep dive into doing it hands-on rather than just reading about it.

---

## 📌 What's Next

This is one lab in an ongoing series as I build toward certifications and an entry-level cybersecurity role. Future additions to this repo will include network security labs, log analysis, and vulnerability scanning projects.

---

## 📫 Let's Connect

I'm actively looking for entry-level opportunities in cybersecurity. If you're hiring, mentoring, or just want to talk shop about career-changing into this field, reach out — I'd love to connect.

*(](https://www.linkedin.com/in/samuel-donkor-9258aa223?utm_source=share_via&utm_content=profile&utm_medium=member_ios) 

/ samuelcyber02@gmail.com
