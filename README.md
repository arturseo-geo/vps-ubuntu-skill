# vps-ubuntu-skill

> Built by **[Artur Ferreira](https://github.com/arturseo-geo)** @ **[The GEO Lab](https://thegeolab.net)**
> [𝕏 @TheGEO_Lab](https://x.com/TheGEO_Lab) · [LinkedIn](https://linkedin.com/in/arturgeo) · [Reddit](https://www.reddit.com/user/Alternative_Teach_74/)

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Licence](https://img.shields.io/badge/licence-MIT-green)
![Reference Docs](https://img.shields.io/badge/reference_docs-8-orange)
![Claude Code](https://img.shields.io/badge/Claude_Code-skill-blueviolet)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)](https://github.com/arturseo-geo/vps-ubuntu-skill/blob/main/CONTRIBUTING.md)

Ubuntu VPS management skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — the full server lifecycle from provisioning to backups: SSH hardening, UFW/fail2ban/iptables, Docker containers, Nginx reverse proxy, SSL/Certbot, PM2, BorgBackup, rclone cloud sync, Monit alerting, Tailscale/WireGuard VPN, and automated maintenance.

## Who This Is For

- **Developers managing their own VPS** who want Claude to handle sysadmin tasks safely
- **Teams deploying Node.js/Python apps** behind Nginx with SSL and PM2
- **Anyone self-hosting** tools, databases, or services on Ubuntu
- **DevOps practitioners** who want a comprehensive reference for common server operations

## What Makes This Different

Server management guides cover one topic. This skill covers the full lifecycle with 8 reference documents:

- ✅ **Firewall management** — UFW, iptables, fail2ban, port management, rate limiting, network diagnostics
- ✅ **Security hardening** — SSH keys, user management, kernel hardening, rkhunter, chkrootkit, ClamAV, auditd, AIDE
- ✅ **Backup strategies** — rsync, BorgBackup, database dumps, rclone to S3/B2/Google Drive/R2, verification
- ✅ **Monitoring & alerting** — disk/memory/CPU monitoring, logwatch, email/Slack/Telegram alerts, Monit, health checks
- ✅ **Cron & scheduling** — crontab syntax, debugging, systemd timers, anacron
- ✅ **Web server** — Nginx reverse proxy patterns, gzip/Brotli, rate limiting, caching, SSL/Certbot, PM2, systemd
- ✅ **Containers** — Docker installation, lifecycle, Compose, networking, image cleanup, Dockerfile best practices
- ✅ **VPN** — Tailscale and WireGuard setup for secure server access
- ✅ **Emergency procedures** — disk full recovery, locked out of SSH, runaway processes
- ✅ **Production-tested** — patterns used to manage 5 production services at The GEO Lab

## Install

```bash
# Clone
git clone https://github.com/arturseo-geo/vps-ubuntu-skill.git ~/.claude/skills/vps-ubuntu

# Or install all 12 skills at once
git clone https://github.com/arturseo-geo/claude-code-skills.git
cp -r claude-code-skills/skills/vps-ubuntu ~/.claude/skills/
```

## File Structure

```
vps-ubuntu-skill/
├── SKILL.md                  — Core skill: provisioning, diagnostics, emergency procedures, safety rules
├── references/
│   ├── firewall.md           — UFW, iptables, fail2ban, port management, rate limiting
│   ├── security.md           — SSH hardening, rkhunter, chkrootkit, ClamAV, auditd, AIDE
│   ├── backups.md            — rsync, BorgBackup, rclone cloud sync, database backups, verification
│   ├── monitoring.md         — Disk/memory/CPU, logwatch, alerting, health checks, Monit
│   ├── cron.md               — Crontab syntax, debugging, systemd timers, anacron
│   ├── webserver.md          — Nginx reverse proxy, compression, caching, SSL/Certbot, PM2, systemd
│   └── containers.md         — Docker, Compose, networking, image cleanup, security
└── .github/                  — Issue templates and PR template
```

## Related Repos

- [claude-code-skills](https://github.com/arturseo-geo/claude-code-skills) — Full collection of 12 skills

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines. PRs welcome.

---

Built and maintained by **[Artur Ferreira](https://github.com/arturseo-geo)** @ **[The GEO Lab](https://thegeolab.net)** · [MIT License](LICENSE)
