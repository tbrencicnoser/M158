# Aufgabe 2 – Architekturdiagramm erstellen

## ✅ Stufe 1 – Vollständige Darstellung der Soll-Systemkomponenten

```plaintext
+----------------+        +------------------+        +--------------------+
|    Client      |  -->   |   Webserver      |  -->   |     DB-Server      |
|  (Browser)     |        |  Apache + PHP    |        |  MySQL/MariaDB     |
+----------------+        +------------------+        +--------------------+
                              |        ↑
                              v        |
                         phpMyAdmin / Adminer
```

- Komponenten:
  - **Client**: Greift per HTTP/HTTPS auf den Webserver zu
  - **Webserver**: Apache2 + PHP
  - **DB-Server**: MariaDB oder MySQL
  - **phpMyAdmin/Adminer**: zur DB-Verwaltung via Web

## ✅ Stufe 2 – FQDN, IP-Adressen, AWS-Infos (lokal simuliert)

| Komponente         | IP-Adresse     | Hostname/FQDN                   | AWS-Info               |
|--------------------|----------------|----------------------------------|------------------------|
| Webserver          | 192.168.56.10  | webserver.migration.local       | EC2 (simuliert lokal)  |
| Datenbank-Server   | 192.168.56.11  | db.migration.local              | RDS (simuliert lokal)  |
| phpMyAdmin         | 192.168.56.10  | webserver.migration.local/phpmyadmin | –                |

## ✅ Stufe 3 – Struktur mit Farben (ASCII-Farblegende)

Farblegende:
- 🔵 Webserver-Komponenten
- 🟢 Datenbank
- 🟡 Benutzer

```plaintext
     🟡 Benutzer (Browser)
             │
             ▼
    🔵 Apache2 + PHP (webserver.migration.local)
             │
             ▼
    🔵 phpMyAdmin (gleicher Host)
             │
             ▼
    🟢 MySQL/MariaDB (db.migration.local)
```
