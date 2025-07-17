# Aufgabe 9 – FTP-Zugang einrichten

## ✅ Stufe 1 – Sicherer FTP-Zugriff (FTPS)

Ich habe den vsftpd-Server installiert und für FTPS (FTP über TLS) konfiguriert:

```bash
sudo apt install vsftpd openssl
```

### SSL-Zertifikat generieren:
```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/vsftpd.key \
  -out /etc/ssl/certs/vsftpd.crt
```

### Konfiguration anpassen:
```bash
sudo nano /etc/vsftpd.conf
```

Relevante Änderungen:
```ini
ssl_enable=YES
rsa_cert_file=/etc/ssl/certs/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
```

Dienst neu starten:
```bash
sudo systemctl restart vsftpd
```

Zugriff über: `ftps://tomas-migration.no-ip.org`

## ✅ Stufe 2 – Benutzer mit beschränktem Zugriff

Ein Benutzer wurde speziell für FTP-Zugriff eingerichtet:

```bash
sudo useradd -m ftpuser -s /sbin/nologin
sudo passwd ftpuser
```

Zugriffsrechte gesetzt:
```bash
sudo mkdir /var/www/wordpress/wp-content/uploads
sudo chown ftpuser:ftpuser /var/www/wordpress/wp-content/uploads
```

`vsftpd.conf`:
```ini
chroot_local_user=YES
allow_writeable_chroot=YES
```

Der Benutzer kann sich nun ausschließlich im Upload-Verzeichnis bewegen, Uploads machen, aber nicht in andere Verzeichnisse wechseln. Maximale Sicherheit ist gewährleistet.
