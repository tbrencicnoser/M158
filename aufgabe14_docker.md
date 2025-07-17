# Aufgabe 14 – Docker verwenden

## ✅ Stufe 1 – < 2 Komponenten mit Docker Compose umgesetzt

Ich habe Webserver (Apache + PHP) und Datenbank (MariaDB) in Containern bereitgestellt.

### docker-compose.yml:
```yaml
version: '3.8'

services:
  wordpress:
    image: wordpress:latest
    ports:
      - "80:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wp_user
      WORDPRESS_DB_PASSWORD: securepassword
      WORDPRESS_DB_NAME: wordpress_db
    volumes:
      - wordpress_data:/var/www/html

  db:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_DATABASE: wordpress_db
      MYSQL_USER: wp_user
      MYSQL_PASSWORD: securepassword
      MYSQL_ROOT_PASSWORD: rootpassword
    volumes:
      - db_data:/var/lib/mysql

volumes:
  wordpress_data:
  db_data:
```

Start:
```bash
docker-compose up -d
```

## ✅ Stufe 2 – < 6 Komponenten

Ich habe zusätzlich phpMyAdmin und einen Mailhog-Container für Tests eingebunden:

```yaml
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
      - "8080:80"
    environment:
      PMA_HOST: db

  mailhog:
    image: mailhog/mailhog
    ports:
      - "8025:8025"
```

Erreichbar unter:
- `http://localhost:8080` → phpMyAdmin
- `http://localhost:8025` → Mailhog

## ✅ Stufe 3 – Alle Komponenten dockerisiert

Zusätzlich wurde ein Nginx-Reverse-Proxy und ein Cronjob-Container für Backups hinzugefügt:

```yaml
  nginx:
    image: nginx:latest
    ports:
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf

  backup:
    build: ./backup
    volumes:
      - wordpress_data:/data
```

Ergebnis:
- Komplette Umgebung in Docker umgesetzt
- Einfach skalierbar
- Lokal und in der Cloud lauffähig
