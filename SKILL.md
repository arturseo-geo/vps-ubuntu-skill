---
name: vps-ubuntu
description: >
  Manage, secure, monitor, and maintain Ubuntu VPS servers. Use this skill
  whenever the user mentions VPS, Ubuntu server, Linux server, firewall, UFW,
  iptables, fail2ban, SSH hardening, security hardening, server security,
  intrusion detection, rootkit detection, rkhunter, chkrootkit, ClamAV, auditd,
  server backups, rsync backup, borgbackup, automated backups, rclone, cron jobs,
  crontab, scheduled tasks, disk space, df, du, disk usage, out of disk,
  memory usage, swap, RAM, server monitoring, htop, netstat, ss, open ports,
  system health, server performance, log rotation, logwatch, unattended upgrades,
  automatic updates, server hardening, sysctl, kernel parameters, brute force
  protection, Nginx, Apache, SSL certificates, Certbot, Let's Encrypt, PM2,
  systemd services, process management, server deployment, Docker, containers,
  Docker Compose, Tailscale, WireGuard, VPN, server provisioning, or any task
  involving managing a Linux/Ubuntu VPS or dedicated server.
---

# VPS Ubuntu Management Skill

This skill covers the full lifecycle of Ubuntu VPS management.
Load the relevant reference file for detailed commands:

| Topic | Reference file | Load when... |
|---|---|---|
| Firewall & network | `references/firewall.md` | UFW, iptables, open ports, rate limiting |
| Security hardening | `references/security.md` | SSH, fail2ban, kernel params, auditing, rootkits, ClamAV |
| Backups | `references/backups.md` | rsync, Borg, rclone, cloud sync, backup testing |
| GEO Lab full clone | `references/geolab-backup.md` | "full backup", "clone backup", "100% backup", "snapshot" — exact 8-step verified procedure |
| Monitoring & alerts | `references/monitoring.md` | disk, memory, CPU, log analysis, alerting, health checks |
| Cron jobs | `references/cron.md` | crontab syntax, scheduling, debugging, systemd timers |
| Web server | `references/webserver.md` | Nginx, SSL, PM2, reverse proxy, compression, rate limiting |
| Containers | `references/containers.md` | Docker, Docker Compose, networking, image cleanup |

---

## Server Provisioning — Fresh Ubuntu VPS

Run these steps immediately after first SSH login to a new server:

```bash
# 1. Update system
apt update && apt upgrade -y

# 2. Set timezone
timedatectl set-timezone UTC

# 3. Create non-root user (if needed)
adduser deploy
usermod -aG sudo deploy

# 4. Harden SSH
sed -i 's/#PermitRootLogin yes/PermitRootLogin prohibit-password/' /etc/ssh/sshd_config
sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart sshd

# 5. Enable firewall
ufw default deny incoming
ufw default allow outgoing
ufw allow 22/tcp    # SSH
ufw allow 80/tcp    # HTTP
ufw allow 443/tcp   # HTTPS
ufw --force enable

# 6. Install fail2ban
apt install -y fail2ban
systemctl enable fail2ban
systemctl start fail2ban

# 7. Enable automatic security updates
apt install -y unattended-upgrades
dpkg-reconfigure -plow unattended-upgrades

# 8. Install common tools
apt install -y curl wget git htop ncdu tree jq
```

## Quick Diagnostics

```bash
# System overview
htop                              # CPU, memory, processes
df -h                              # Disk usage
free -m                            # Memory
uptime                             # Load average
ss -tlnp                           # Open ports
journalctl -p err --since today    # Today's errors

# Service status
systemctl status nginx
systemctl status redis-server
systemctl status postgresql
pm2 list                           # PM2 processes
pm2 logs <name> --lines 50         # Recent logs

# Network
curl -s ifconfig.me                # Public IP
ss -s                              # Socket statistics
```

## Emergency Procedures

### Disk full
```bash
# Find large files
ncdu /                             # Interactive disk usage
find / -type f -size +100M 2>/dev/null | head -20

# Quick cleanup
apt autoremove -y
journalctl --vacuum-size=50M
rm -rf /tmp/*
pm2 flush                          # Clear PM2 logs
```

### Locked out of SSH
1. Use DigitalOcean console (droplet > Access > Console)
2. Check `/var/log/auth.log` for fail2ban blocks
3. `fail2ban-client set sshd unbanip YOUR_IP`
4. Or use Tailscale if configured

### Runaway process
```bash
top -o %CPU                        # Find by CPU
top -o %MEM                        # Find by memory
kill -15 <PID>                     # Graceful stop
kill -9 <PID>                      # Force kill
pm2 restart <name>                 # Restart PM2 process
```

## Safety Rules

- ALWAYS confirm before running destructive commands (rm -rf, DROP TABLE)
- ALWAYS backup before modifying nginx configs: `cp file file.bak.$(date +%s)`
- ALWAYS test nginx before reload: `nginx -t && systemctl reload nginx`
- NEVER restart nginx/MySQL without confirming no active connections
- NEVER modify system files without a backup
- PREFER `systemctl reload` over `systemctl restart` when possible
