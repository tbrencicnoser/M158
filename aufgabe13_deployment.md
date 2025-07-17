# Aufgabe 13 – Deployment automatisieren

## ✅ Stufe 1 – Auto-Deployment über CI/CD eingerichtet

Ich habe GitHub Actions genutzt, um beim Push ins Repository ein automatisches Deployment per SCP auf den Webserver auszulösen.

`.github/workflows/deploy.yml`:
```yaml
name: Deploy to Webserver

on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2

      - name: Deploy via SCP
        uses: appleboy/scp-action@master
        with:
          host: ${{ secrets.HOST }}
          username: ${{ secrets.USER }}
          password: ${{ secrets.PASS }}
          source: "."
          target: "/var/www/wordpress"
```

Secrets (`HOST`, `USER`, `PASS`) sind im Repository hinterlegt.

## ✅ Stufe 2 – Staging- & Live-Branch

- `main` = Live
- `staging` = Preview/Entwicklung

Workflow für Staging:
```yaml
on:
  push:
    branches: [ "staging" ]
```

Unterschiedliche Pfade:
- `main` → `/var/www/wordpress`
- `staging` → `/var/www/wordpress-staging`

## ✅ Stufe 3 – Eigenes Plugin mit Umgebungsvariablen

Ich habe ein einfaches WordPress-Plugin erstellt, das je nach Umgebung automatisch Konfigurationen lädt:

```php
<?php
/*
Plugin Name: WP Environment Loader
*/

if (getenv('WP_ENV') === 'staging') {
    define('WP_DEBUG', true);
    define('WP_SITEURL', 'https://staging.tomas-migration.no-ip.org');
} else {
    define('WP_DEBUG', false);
    define('WP_SITEURL', 'https://tomas-migration.no-ip.org');
}
?>
```

Das Plugin erkennt `WP_ENV` und passt Verhalten an. Damit sind beide Umgebungen (LIVE & STAGE) intelligent steuerbar.
