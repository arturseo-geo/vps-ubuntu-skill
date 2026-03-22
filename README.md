# vps-ubuntu-skill

> **Also available as part of [claude-code-skills](https://github.com/arturseo-geo/claude-code-skills)** — a collection of 12 production-tested skills for Claude Code.

> Built by **[Artur Ferreira](https://github.com/arturseo-geo)** @ **[The GEO Lab](https://thegeolab.net)**
> [X @TheGEO_Lab](https://x.com/TheGEO_Lab) · [LinkedIn](https://linkedin.com/in/arturgeo) · [Reddit](https://www.reddit.com/user/Alternative_Teach_74/)

![Licence](https://img.shields.io/badge/licence-MIT-green)
![Claude Code](https://img.shields.io/badge/Claude_Code-skill-blueviolet)

Manage, secure, monitor, and maintain Ubuntu VPS servers. Covers the full lifecycle from provisioning to backups, including firewall management, SSH hardening, Docker containers, Nginx reverse proxy, SSL certificates, alerting, and automated maintenance.

## Install

```bash
git clone https://github.com/arturseo-geo/vps-ubuntu-skill.git ~/.claude/skills/vps-ubuntu
```

## File Structure

- `SKILL.md` — Core skill instructions: provisioning, diagnostics, emergency procedures, safety rules, Tailscale/WireGuard VPN, unattended upgrades
- `references/firewall.md` — UFW, iptables, fail2ban, port management, rate limiting, network diagnostics
- `references/security.md` — SSH hardening, user management, kernel hardening, rkhunter, chkrootkit, ClamAV, auditd, AIDE, file integrity
- `references/backups.md` — rsync, BorgBackup, database backups, rclone cloud sync (S3, B2, Google Drive, R2), backup verification
- `references/monitoring.md` — Disk, memory, CPU monitoring, log analysis, logwatch, email/Slack/Telegram alerting, health check endpoints, Monit
- `references/cron.md` — Crontab syntax, scheduling, debugging, systemd timers, anacron
- `references/webserver.md` — Nginx reverse proxy patterns, gzip/Brotli compression, rate limiting, caching, SSL/Certbot, PM2, systemd services
- `references/containers.md` — Docker installation, container lifecycle, Docker Compose, networking, image cleanup, Dockerfile best practices, security
- `CONTRIBUTING.md` — Contribution guidelines
- `SECURITY.md` — Security policy
- `.github/ISSUE_TEMPLATE/bug-report.md` — Bug report template
- `.github/ISSUE_TEMPLATE/platform-update.md` — Ubuntu/tool version update template
- `.github/pull_request_template.md` — PR template

## Related Repos

- [claude-code-skills](https://github.com/arturseo-geo/claude-code-skills) — Full collection of 12 skills
- [mcp-wordpress-setup](https://github.com/arturseo-geo/mcp-wordpress-setup) — WordPress MCP server setup

## Acknowledgments

Built following the open-source best practice approach — reading community work for inspiration, writing original content, and crediting every source.

**Based on:**
- [Agent Skills specification](https://github.com/anthropics/skills) by Anthropic (Apache 2.0)

All skill content is original writing. No files were copied or adapted from any source.

## Author

Built and maintained by **[Artur Ferreira](https://github.com/arturseo-geo)** @ **[The GEO Lab](https://thegeolab.net)**

## License

[MIT](LICENSE)
