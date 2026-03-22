# Contributing to vps-ubuntu-skill

Thank you for helping improve this Claude Code skill. Here's how to contribute effectively.

## How to Contribute

### Reporting Issues
- **Bugs**: Use the [Bug Report](.github/ISSUE_TEMPLATE/bug-report.md) template
- **Tool/platform updates**: Use the [Platform Update](.github/ISSUE_TEMPLATE/platform-update.md) template — tools change defaults, deprecate flags, and introduce new features frequently. Keeping commands current is one of the most valuable contributions.

### Submitting Changes
1. Fork the repository
2. Create a feature branch (`git checkout -b update/docker-compose-v2-syntax`)
3. Make your changes
4. Test with Claude Code to verify the skill works as expected
5. Submit a pull request using the [PR template](.github/pull_request_template.md)

## What We're Looking For

### High-Value Contributions
- **Ubuntu version updates**: New LTS releases, changed defaults, new package names
- **Tool updates**: Docker, Nginx, Certbot, fail2ban, UFW command changes
- **Security advisories**: New hardening recommendations, deprecated ciphers, CVE mitigations
- **New reference areas**: Topics not yet covered (e.g., PostgreSQL tuning, Redis hardening)
- **Improved procedures**: Better backup scripts, monitoring patterns, automation
- **Real-world fixes**: If you hit a gotcha on a VPS that the skill doesn't warn about, add it

### Writing Style
- Be concise and actionable — every line should help Claude manage a server correctly
- Use specific commands over vague advice (`ufw limit ssh` not "configure rate limiting")
- Include the full command with flags, not just the tool name
- Always show how to test/verify a change worked (e.g., `nginx -t` after config edits)
- Mark destructive commands clearly (data loss, lockout risk, downtime)
- Structure with headers, code blocks, and tables for scannability
- Write for Claude as the reader — clear instructions it can follow precisely

### What to Avoid
- Untested commands (always verify on Ubuntu 22.04+ or 24.04+)
- Commands that assume a specific VPS provider without noting the assumption
- Removing existing content without a clear reason and replacement
- Adding tools without explaining when to use them vs existing alternatives

## File Structure

| File | Purpose |
|---|---|
| `SKILL.md` | Core skill instructions — the main file Claude reads |
| `references/firewall.md` | UFW, iptables, fail2ban, network diagnostics |
| `references/security.md` | SSH hardening, rootkit detection, auditd, ClamAV |
| `references/backups.md` | rsync, Borg, rclone, cloud sync, verification |
| `references/monitoring.md` | Disk, memory, CPU, logs, alerting, health checks |
| `references/cron.md` | Crontab, systemd timers, debugging |
| `references/webserver.md` | Nginx, SSL, PM2, systemd services, compression |
| `references/containers.md` | Docker, Docker Compose, networking, cleanup |

## Testing Your Changes

The best way to test is to install the skill in Claude Code and run through common server management tasks:

1. Copy the updated skill to `~/.claude/skills/vps-ubuntu/`
2. Start a Claude Code session
3. Ask Claude to perform tasks related to your changes (e.g., "set up Docker Compose for a Node app with Postgres")
4. Verify the output follows your updated guidelines and commands work on a real server

## Code of Conduct

Be respectful, constructive, and focused on making the skill better. We welcome contributors of all experience levels.
