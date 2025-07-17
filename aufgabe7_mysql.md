# Aufgabe 7 – MySQL/MariaDB aufsetzen

## ✅ Stufe 1 – WordPress-spezifischer Datenbankbenutzer

1. MySQL/MariaDB installiert:
```bash
sudo apt install mariadb-server
sudo systemctl start mariadb
```

2. Datenbank und Benutzer angelegt:
```sql
CREATE DATABASE wordpress_db DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
CREATE USER 'wp_user'@'%' IDENTIFIED BY 'securepassword';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wp_user'@'%';
FLUSH PRIVILEGES;
```

> Hinweis: Der Benutzer darf von allen Hosts (`%`) zugreifen.

## ✅ Stufe 2 – Root-Zugriff nur lokal

1. Root-Zugriff beschränkt:
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'rootpassword';
DELETE FROM mysql.user WHERE User='root' AND Host!='localhost';
FLUSH PRIVILEGES;
```

2. Test:
```bash
mysql -u root -p   # funktioniert lokal
mysql -h <ip> -u root -p   # wird verweigert
```

## ✅ Stufe 3 – Dedizierter DB-Server

In meiner Testumgebung verwende ich eine **zweite VM** (192.168.56.11) ausschließlich als DB-Server.

- Firewall-Einstellung:
```bash
sudo ufw allow from 192.168.56.10 to any port 3306
```

- `/etc/mysql/mariadb.conf.d/50-server.cnf` angepasst:
```ini
bind-address = 192.168.56.11
```

- WordPress auf Webserver (192.168.56.10) nutzt:
```php
define( 'DB_HOST', '192.168.56.11' );
```

Test mit `telnet 192.168.56.11 3306` zeigt: Verbindung erfolgreich.

So ist der Datenbankserver vollständig getrennt vom Webserver (Produktionsszenario).
