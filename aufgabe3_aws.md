# Aufgabe 3 – AWS-Umgebung einrichten

## ✅ Stufe 1 – Umgebung funktioniert (Zugriff via SSH)

Da ich lokal arbeite, habe ich eine virtuelle Testumgebung erstellt, die AWS simuliert:

- Betriebssystem: Ubuntu Server 22.04 LTS (lokale VM mit VirtualBox)
- SSH-Zugriff:
  ```bash
  ssh tomas@192.168.56.10
  ```

## ✅ Stufe 2 – Umgebung mit sämtlichen Angaben aus der Planung

| Komponente     | IP-Adresse     | Rolle                  | Beschreibung                               |
|----------------|----------------|------------------------|--------------------------------------------|
| Webserver      | 192.168.56.10  | Apache + PHP           | Hosten der WordPress-Seite                 |
| Datenbank      | 192.168.56.11  | MariaDB/MySQL          | Speichert Inhalte und Benutzer             |
| Verwaltung     | –              | SSH                    | Verwaltung über Terminal möglich           |

Alle Instanzen sind betriebsbereit, Kommunikation funktioniert:

- Der Webserver kann mit `ping 192.168.56.11` die Datenbank erreichen.
- Die WordPress-Installation funktioniert (wird in Aufgabe 10 beschrieben).
- Alle Installationsschritte wurden dokumentiert:
  ```bash
  sudo apt update
  sudo apt install apache2 mariadb-server php libapache2-mod-php php-mysql
  ```

Für SSH wurden statische IPs, Benutzer mit SSH-Key-Login und Firewall-Freigaben eingerichtet.
