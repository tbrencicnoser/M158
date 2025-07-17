# Aufgabe 8 – Web-Datenbanktool (phpMyAdmin/Adminer)

## ✅ Stufe 1 – Standard-Installation

Ich habe phpMyAdmin als Web-Datenbanktool installiert:

```bash
sudo apt install phpmyadmin
```

Installationsoptionen:
- Webserver: Apache2
- Datenbankkonfiguration: Ja
- Passwort gesetzt für `phpmyadmin`-User

Verfügbar unter:
```
http://tomas-migration.no-ip.org/phpmyadmin
```

## ✅ Stufe 2 – Erreichbar über HTTPS und Domainname

Ich habe sichergestellt, dass phpMyAdmin über SSL erreichbar ist:

- `wordpress.conf` angepasst:
```apache
Alias /phpmyadmin /usr/share/phpmyadmin
<Directory /usr/share/phpmyadmin>
    Options FollowSymLinks
    DirectoryIndex index.php
    AllowOverride All
    Require all granted
</Directory>
```

- SSL aktiviert (siehe Aufgabe 5)
- Zugriff über:  
  `https://tomas-migration.no-ip.org/phpmyadmin`

## ✅ Stufe 3 – Dedicated DB-Server verwendet

phpMyAdmin greift auf den dedizierten Datenbankserver (192.168.56.11) zu.

- Konfiguration angepasst:
```bash
sudo nano /etc/phpmyadmin/config.inc.php
```

- Eingefügt:
```php
$cfg['Servers'][$i]['host'] = '192.168.56.11';
$cfg['Servers'][$i]['connect_type'] = 'tcp';
```

- Zugriff erfolgreich getestet mit WordPress-DB-Nutzer.

Damit ist das Web-Tool sicher über HTTPS und auf dedizierten DB-Server ausgerichtet.
