# GEO Lab Full Clone Backup

When user asks for "full backup", "clone backup", "100% backup", or "snapshot" — follow this EXACT procedure. No shortcuts.

## VPS: 100.87.191.9 (Tailscale) / 45.55.91.146 (public)
## Backup destination: C:\Users\jorge\Desktop\VPS_FULL_BACKUP_{DATE}\

---

## Step 1: STOP all services
```bash
ssh root@100.87.191.9 'pm2 stop all && systemctl stop extractability-checker && sleep 3'
```
Services MUST be stopped before copying SQLite databases (WAL corruption risk).

## Step 2: Verify database integrity
```bash
# PostgreSQL
sudo -u postgres pg_dumpall > /tmp/postgres_verified.sql
tail -3 /tmp/postgres_verified.sql  # MUST end with "-- complete"

# Redis — synchronous SAVE, NOT BGSAVE
redis-cli SAVE
cp /var/lib/redis/dump.rdb /tmp/redis_verified.rdb

# SQLite — every .db file MUST return "ok"
for db in $(find /var/www -name "*.db" -type f); do
  echo "$db: $(sqlite3 \"$db\" \"PRAGMA integrity_check;\")"
done
```

## Step 3: Full copy (ALL files including node_modules, venv, .env, .db)
```bash
BACKUP="/tmp/vps-clone-$(date +%Y%m%d)"
mkdir -p $BACKUP/_system/{nginx,ssl,pm2,systemd}

# 7 projects + extractability checker
for dir in seo-intelligence geolab-backlinks geolab-keywords geolab-command-center geolab-geo-os geolab-links geolab-writer; do
  cp -a /var/www/$dir $BACKUP/
done
cp -a /opt/extractability-checker $BACKUP/

# Verified database dumps
cp /tmp/postgres_verified.sql $BACKUP/
cp /tmp/redis_verified.rdb $BACKUP/

# System configs
cp -a /etc/nginx/sites-available/* $BACKUP/_system/nginx/
cp /etc/nginx/nginx.conf $BACKUP/_system/nginx/
cp /etc/nginx/.htpasswd $BACKUP/_system/nginx/htpasswd
cp -rL /etc/letsencrypt/live/ $BACKUP/_system/ssl/
cp /etc/letsencrypt/options-ssl-nginx.conf $BACKUP/_system/ssl/
cp /etc/letsencrypt/ssl-dhparams.pem $BACKUP/_system/ssl/
cp /root/.pm2/dump.pm2 $BACKUP/_system/pm2/
pm2 jlist > $BACKUP/_system/pm2/processes.json
cp /etc/systemd/system/extractability-checker.service $BACKUP/_system/systemd/
```

## Step 4: Generate SHA256 checksums
```bash
cd $BACKUP
sha256sum postgres_verified.sql redis_verified.rdb > CHECKSUMS.sha256
find . -name "*.db" -type f -exec sha256sum {} \; >> CHECKSUMS.sha256
find . -name ".env" -type f -exec sha256sum {} \; >> CHECKSUMS.sha256
```

## Step 5: Create tar + MD5
```bash
cd /tmp
tar czf vps-full-clone-$(date +%Y%m%d).tar.gz $(basename $BACKUP)/
md5sum vps-full-clone-$(date +%Y%m%d).tar.gz
```
Record the MD5 hash.

## Step 6: RESTART all services
```bash
pm2 start all && systemctl start extractability-checker && pm2 save
```
Verify all online: `pm2 list | grep -c online`

## Step 7: Transfer to PC (MUST split for WSL)
WSL scp fails on files >400MB with "Cannot allocate memory". Always split:
```bash
# On VPS
split -b 100M /tmp/vps-full-clone-*.tar.gz /tmp/vps-clone-part-

# On WSL — download each part
DEST="/mnt/c/Users/jorge/Desktop/VPS_FULL_BACKUP_$(date +%Y%m%d)"
mkdir -p "$DEST"
for part in aa ab ac ad ae; do
  scp root@100.87.191.9:/tmp/vps-clone-part-$part "$DEST/"
done

# Reassemble
cat "$DEST"/vps-clone-part-* > "$DEST/vps-full-clone.tar.gz"
rm "$DEST"/vps-clone-part-*
```

## Step 8: Verify on PC
```bash
# MD5 MUST match VPS
md5sum "$DEST/vps-full-clone.tar.gz"

# Test tar integrity
tar tzf "$DEST/vps-full-clone.tar.gz" | wc -l  # should be ~143,000+

# Extract and verify SQLite
tar xzf "$DEST/vps-full-clone.tar.gz" --include="*.db" -C /tmp/
for db in $(find /tmp/vps-clone-* -name "*.db"); do
  sqlite3 "$db" "PRAGMA integrity_check;"
done
```

## Backup Checklist (ALL must be present)
- 7 project dirs with node_modules + venv + .env + .db + data/
- extractability-checker from /opt/
- postgres_verified.sql (ends with "complete")
- redis_verified.rdb (synchronous SAVE)
- 8 .env files
- OAuth tokens: gsc_token, ga4_token, gsc_credentials, ga4_credentials, service-account
- Nginx: all site configs + nginx.conf + .htpasswd
- SSL: /etc/letsencrypt/live/
- PM2: dump.pm2 + processes.json
- systemd: extractability-checker.service
- CHECKSUMS.sha256
- MD5 verified after download

## NEVER do this
- Copy SQLite while services are running
- Use BGSAVE for Redis
- Transfer >400MB in single scp on WSL
- Skip integrity checks
- Skip MD5 verification
- Skip restarting services after backup
