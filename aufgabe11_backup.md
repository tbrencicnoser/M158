# Aufgabe 11 – Backup-Konzept umsetzen

## ✅ Stufe 1 – Backup über CRON inkl. Aufbewahrung

Ich habe ein automatisiertes Backup-Skript erstellt:
```bash
#!/bin/bash
BACKUP_DIR="/var/backups/wp"
DB_NAME="wordpress_db"
DB_USER="wp_user"
DB_PASS="securepassword"
NOW=$(date +%F_%H-%M)

mkdir -p $BACKUP_DIR

# DB Backup
mysqldump -u $DB_USER -p$DB_PASS $DB_NAME > $BACKUP_DIR/db_$NOW.sql

# File Backup
tar czf $BACKUP_DIR/files_$NOW.tar.gz /var/www/wordpress

# Alte Backups nach 7 Tagen löschen
find $BACKUP_DIR -type f -mtime +7 -delete
```

Cronjob eingetragen:
```bash
crontab -e
0 3 * * * /usr/local/bin/backup_wp.sh
```

Ergebnis:
- Tägliches Backup um 03:00 Uhr
- Backups werden 7 Tage aufbewahrt

## ✅ Stufe 2 – Automatischer E-Mail-Versand via SMTP

Skript ergänzt um Mail-Funktion:
```bash
echo "WordPress Backup $NOW erfolgreich erstellt." | mail -s "Backup OK" admin@example.com
```

Vorbereitung:
```bash
sudo apt install mailutils msmtp
```

`~/.msmtprc`:
```ini
defaults
auth on
tls on
tls_trust_file /etc/ssl/certs/ca-certificates.crt
account default
host smtp.example.com
port 587
from admin@example.com
user admin@example.com
password deinpasswort
```

So wird nach jedem Backup automatisch eine Bestätigungsmail gesendet.
