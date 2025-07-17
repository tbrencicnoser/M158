# Aufgabe 10 – WordPress migrieren

## ✅ Stufe 1 – DB migriert, Files korrekt im DocumentRoot

1. WordPress-Quellseite exportiert:
   - Datenbank exportiert per `mysqldump`
   - Webverzeichnis (WordPress-Dateien) per `scp` übertragen

2. Zielsystem:
```bash
sudo cp -r wordpress /var/www/wordpress
sudo chown -R www-data:www-data /var/www/wordpress
```

3. Datenbank importiert:
```bash
mysql -u wp_user -p wordpress_db < dump.sql
```

## ✅ Stufe 2 – wp-config.php & URL-Änderung

`wp-config.php` angepasst:
```php
define( 'DB_NAME', 'wordpress_db' );
define( 'DB_USER', 'wp_user' );
define( 'DB_PASSWORD', 'securepassword' );
define( 'DB_HOST', '192.168.56.11' );
```

In der Datenbank `siteurl` und `home` aktualisiert:
```sql
UPDATE wp_options SET option_value='https://tomas-migration.no-ip.org' WHERE option_name='siteurl';
UPDATE wp_options SET option_value='https://tomas-migration.no-ip.org' WHERE option_name='home';
```

## ✅ Stufe 3 – Domain ersetzen & Benutzer-Login aktivieren

1. Alte Domain ersetzt:
```sql
UPDATE wp_posts SET guid = REPLACE(guid, 'alte-domain', 'tomas-migration.no-ip.org');
UPDATE wp_posts SET post_content = REPLACE(post_content, 'alte-domain', 'tomas-migration.no-ip.org');
UPDATE wp_postmeta SET meta_value = REPLACE(meta_value, 'alte-domain', 'tomas-migration.no-ip.org');
```

Alternativ: Plugin **Better Search Replace** verwenden.

2. Benutzer-Login repariert (Passwort durch MD5 ersetzt):
```sql
UPDATE wp_users SET user_pass = MD5('neuespasswort') WHERE user_login = 'admin';
```

Ergebnis:
- WordPress vollständig migriert
- Neue Domain ersetzt alte
- Login erfolgreich
