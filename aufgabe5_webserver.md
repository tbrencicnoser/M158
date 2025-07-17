# Aufgabe 5 – Webserver konfigurieren

## ✅ Stufe 1 – Virtual Hosts & Rewrite-Engine

Ich habe Virtual Hosts für meine Domain konfiguriert und die Rewrite-Engine aktiviert:

1. Neue Konfigurationsdatei erstellt:
   ```bash
   sudo nano /etc/apache2/sites-available/wordpress.conf
   ```

2. Inhalt:
   ```apache
   <VirtualHost *:80>
       ServerName tomas-migration.no-ip.org
       DocumentRoot /var/www/wordpress
       <Directory /var/www/wordpress>
           AllowOverride All
       </Directory>
   </VirtualHost>
   ```

3. Rewrite-Engine aktiviert:
   ```bash
   sudo a2enmod rewrite
   sudo systemctl restart apache2
   ```

4. Aktivierung des Virtual Hosts:
   ```bash
   sudo a2ensite wordpress.conf
   sudo systemctl reload apache2
   ```

## ✅ Stufe 2 – SSL (HTTPS) aktiviert mit Self-Signed Certificate

1. Zertifikat erstellt:
   ```bash
   sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
       -keyout /etc/ssl/private/apache-selfsigned.key \
       -out /etc/ssl/certs/apache-selfsigned.crt
   ```

2. HTTPS-Config ergänzt:
   ```apache
   <VirtualHost *:443>
       ServerName tomas-migration.no-ip.org
       DocumentRoot /var/www/wordpress
       SSLEngine on
       SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
       SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
   </VirtualHost>
   ```

3. Module aktivieren und Apache neustarten:
   ```bash
   sudo a2enmod ssl
   sudo systemctl restart apache2
   ```

## ✅ Stufe 3 – HTTP auf HTTPS Weiterleitung & keine Default Page

1. Redirect in Port-80 Config:
   ```apache
   <VirtualHost *:80>
       ServerName tomas-migration.no-ip.org
       Redirect / https://tomas-migration.no-ip.org/
   </VirtualHost>
   ```

2. Apache Default Page deaktiviert:
   ```bash
   sudo a2dissite 000-default.conf
   sudo systemctl reload apache2
   ```

**Ergebnis:** Zugriff per HTTP leitet zuverlässig auf HTTPS weiter. Nur noch WordPress erreichbar.
