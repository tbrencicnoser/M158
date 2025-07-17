# Aufgabe 6 – PHP einrichten

## ✅ Stufe 1 – PHP-Funktion phpinfo()

Zur Überprüfung der PHP-Konfiguration wurde eine Datei erstellt:

- Pfad: `/var/www/wordpress/info.php`
- Inhalt:
  ```php
  <?php phpinfo(); ?>
  ```

- Aufruf über Browser:  
  `http://tomas-migration.no-ip.org/info.php`

PHP-Version:
```bash
php -v
# PHP 8.1.x (currently supported)
```

## ✅ Stufe 2 – PHP.ini angepasst

Konfigurationsdatei bearbeitet:
```bash
sudo nano /etc/php/8.1/apache2/php.ini
```

Folgende Parameter wurden angepasst:
```ini
memory_limit = 256M
upload_max_filesize = 64M
post_max_size = 64M
max_execution_time = 120
```

Apache neu gestartet:
```bash
sudo systemctl restart apache2
```

## ✅ Stufe 3 – PHP-FPM (FastCGI Process Manager)

1. PHP-FPM installiert:
```bash
sudo apt install php8.1-fpm libapache2-mod-fcgid
```

2. Apache für FPM vorbereitet:
```bash
sudo a2enmod proxy_fcgi setenvif
sudo a2enconf php8.1-fpm
sudo systemctl restart apache2
```

3. Ergebnis prüfen:
- `ps aux | grep php-fpm` zeigt laufende FPM-Prozesse
- WordPress funktioniert stabil über PHP-FPM

Die Nutzung von PHP-FPM verbessert die Performance und die Ausfallsicherheit.
