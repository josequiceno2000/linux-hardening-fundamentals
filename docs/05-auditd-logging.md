# 05 Audit Logging with auditd

## 01 Mission Overview
Goal: Configure auditd to record security-relevant events for a hardened Linux host.
Real-world mirror: baseline telemetry for incident response and forensic readiness on a production Linux server.

## 02 Environment
- OS: Ubuntu 22.04 (per instance)
- Services: sshd, UFW, fail2ban, auditd
- Audit tools: auditctl, ausearch

## 03 What I Found
- auditd was not configured with custom rules for `/etc` access, privilege escalation, and login telemetry.
- Need: demonstrate rule loading + verify events using `ausearch -k`.

## 04 What I Did (step-by-step)
1) Install auditd
```bash
sudo apt update
sudo apt install -y auditd audispd-plugins
sudo systemctl enable --now auditd
```

2) Add audit rules
- Created: `/etc