# Aufgabe 4 – DNS-Konfiguration

## ✅ Stufe 2 – Webserver öffentlich über Domain erreichbar (simuliert mit No-IP)

Ich habe einen kostenlosen dynamischen DNS-Dienst verwendet, um meinem Webserver eine öffentlich erreichbare Domain zuzuweisen:

- Anbieter: [No-IP](https://www.noip.com/)
- Domain: `tomas-migration.no-ip.org`
- Portweiterleitung: Im Router ist Port 80 (HTTP) und 443 (HTTPS) auf die lokale IP `192.168.56.10` weitergeleitet.

### Umsetzung:

1. Konto bei No-IP erstellt.
2. Dynamischer Hostname `tomas-migration.no-ip.org` registriert.
3. DUC (Dynamic Update Client) installiert, um IP aktuell zu halten:
   ```bash
   sudo apt install noip2
   sudo noip2 -C
   ```
4. Apache-Konfiguration angepasst:
   ```bash
   ServerName tomas-migration.no-ip.org
   ```

### Test:
Die Seite war über `http://tomas-migration.no-ip.org` erreichbar (wenn Portweiterleitung aktiv).

**Hinweis**: Diese Lösung funktioniert auch ohne echten DNS-Server und ist ausreichend für Stufe 2.
