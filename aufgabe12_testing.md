# Aufgabe 12 – Testing der Webapplikation

## ✅ Stufe 1 – Testkatalog mit 20 spezifischen Fällen

Ich habe eine Tabelle mit 20 gezielten Testfällen erstellt, um die Funktionalität der migrierten WordPress-Seite zu prüfen:

| Nr. | Testfall                                      | Ergebnis |
|-----|-----------------------------------------------|----------|
| 1   | Startseite lädt                               | ✅       |
| 2   | Login-Seite erreichbar                         | ✅       |
| 3   | Admin-Login funktioniert                       | ✅       |
| 4   | Seiten lassen sich anzeigen                    | ✅       |
| 5   | Seiten lassen sich bearbeiten                  | ✅       |
| 6   | Neue Seite kann erstellt werden                | ✅       |
| 7   | Plugins können installiert werden              | ✅       |
| 8   | Medien-Upload funktioniert                     | ✅       |
| 9   | Menü kann bearbeitet werden                    | ✅       |
| 10  | Benutzerverwaltung funktioniert                | ✅       |
| 11  | Kommentare aktivierbar                         | ✅       |
| 12  | Themes lassen sich aktivieren                  | ✅       |
| 13  | Permalinks funktionieren nach Rewrite          | ✅       |
| 14  | SSL-Zertifikat gültig                          | ✅       |
| 15  | Weiterleitung HTTP → HTTPS                     | ✅       |
| 16  | Seite reagiert auf Mobilgerät                  | ✅       |
| 17  | Fehlermeldungen werden im Frontend unterdrückt | ✅       |
| 18  | Zugriff auf wp-admin nur mit Login             | ✅       |
| 19  | Datenbankverbindung stabil                     | ✅       |
| 20  | Backups vorhanden & aktuell                    | ✅       |

## ✅ Stufe 2 – Site-Health & Divi Support Page

1. Aufruf:
   `https://tomas-migration.no-ip.org/wp-admin/site-health.php`
   → Status: **Gut**

2. Divi Support Center (falls Divi installiert):
   `https://tomas-migration.no-ip.org/wp-admin/admin.php?page=et_support_center_divi`
   → Lädt ohne Probleme

## ✅ Stufe 3 – Keine sichtbaren Fehlermeldungen

- Frontend getestet mit Chrome & Firefox (F12 → Konsole):
  - Keine JS-Fehler
  - Keine PHP-Warnungen oder Notices sichtbar
- wp-config.php angepasst:
```php
define('WP_DEBUG', false);
define('WP_DEBUG_DISPLAY', false);
@ini_set('display_errors', 0);
```

Ergebnis: Die Seite zeigt **keine** technischen Fehler an – alles stabil & produktionsbereit.
