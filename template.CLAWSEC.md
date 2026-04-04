# ClawSec Rules of Engagement (RoE) Template

This file governs the overarching operational boundaries for ClawSec. The meta-agent parses these directives before executing any penetration testing workflows.
Clone this file to `.clawsec/CLAWSEC.md` or `CLAWSEC.md` in your current working directory to activate it.

## 🎯 Target Scope
- **Authorized Subnets:** `10.0.0.0/24`, `192.168.1.5`
- **Out-of-Bounds:** `10.0.0.1` (Domain Controller - DO NOT TOUCH), `*.production.internal`

## 🛡️ Methodology Constraints
- **Scanning:** Limit Nmap timing to `-T3` to avoid triggering internal SOC alerts.
- **Exploitation:** Do NOT execute denial-of-service (DoS) exploits. If a vulnerable service is identified, attempt safe remote code execution (RCE) exclusively via non-destructive payloads (e.g., executing `whoami` or spawning an encrypted reverse shell).
- **Post-Exploitation:** You may extract SAM hashes but do NOT attempt to change any underlying user passwords.

## 📝 Reporting Directives
- Log all successful exploitation paths into an absolute, structured markdown file in `/tmp/clawsec_report.md`.
