---
name: Privilege Escalation
description: Post-exploitation maneuvers for climbing from low-privileged shells to Root / SYSTEM access safely.
---

# 🔓 Local Privilege Escalation (Post-Exploitation)

You are now operating under the `priv-esc` skill module. Achieving an initial foothold (user shell) is only phase one. Your objective is absolute lateral movement and vertical escalation to `root` (Linux) or `SYSTEM` (Windows).

## 🐧 Linux Exploitation Path

1. **System Enumeration Basics:**
   - `uname -a` (Check kernel version for known bypasses like DirtyCow, PwnKit, DirtyPipe).
   - `sudo -l` (Can this user run specific binaries as root without a password?)
2. **SUID / SGID Hunts:**
   - Run: `find / -perm -u=s -type f 2>/dev/null`
   - Cross-reference the discovered binaries against [GTFOBins](https://gtfobins.github.io/) to break out of restricted environments.
3. **Cronjobs & Timers:**
   - Inspect `/etc/crontab` and `/var/spool/cron`. Look for wildcard injection points or writable bash scripts executing under root.
4. **Automated Enumeration (If Available):**
   - Download/execute `linpeas.sh` or `lse.sh` in `/dev/shm` to find esoteric permission flaws. 

## 🪟 Windows Exploitation Path

1. **Token Privileges:**
   - Run `whoami /priv`. If `SeImpersonatePrivilege` or `SeAssignPrimaryToken` is enabled, deploy a Potato attack (e.g., GodPotato, JuicyPotato) instantly.
2. **Unquoted Service Paths & Insecure Permissions:**
   - Enum services with `wmic service get name,displayname,pathname,startmode`
   - Check ACLs with `icacls`. Look for `SERVICE_CHANGE_CONFIG` rights on high-privilege services.
3. **Credential Harvesting:**
   - Dump SAM hashes if possible. 
   - Parse `C:\Users\*\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt` for plain-text admin credentials.
   - Utilize `RunExploitScript` to invoke PowerShell modules (like PowerUp or BloodHound collectors).

## 🔒 Post-Exploitation Persistence & Cleanup

- If you establish a root/SYSTEM beacon, ensure it operates over TLS or encrypted reverse tunneling.
- Do NOT alter user passwords. Do NOT delete system logs arbitrarily. You are extracting proof of concept flags, mapping domain structures, and escalating context cleanly.
