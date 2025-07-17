# Projektdokumentation – M158 LB2  
## WordPress-Webserver-Migration  
**Tomas Brencic – Klasse PE23f**

---

## Aufgabe 1 – Projektplan erstellen

### ✅ Stufe 1 – Strukturierter Projektplan (Mermaid-Diagramm)

```mermaid
gantt
    title Projektplan WordPress-Migration – Tomas Brencic
    dateFormat  DD.MM.YYYY
    section Vorbereitung
    Idee & Setup vorbereiten     :a1, 01.07.2025, 2d
    Git-Repo + Projektstruktur   :a2, after a1, 0.5d
    section Infrastruktur
    Webserver einrichten (Apache, PHP, MySQL) :a3, 03.07.2025, 1d
    WordPress migrieren          :a4, after a3, 1d
    section Dienste & Sicherheit
    SSL aktivieren + Weiterleitung    :a5, 07.07.2025, 1d
    FTP + Benutzerverwaltung           :a6, after a5, 0.5d
    Backups automatisieren 🟩          :milestone, a6, 08.07.2025
    section Tests & Feinschliff
    Funktionstests durchführen   :a7, 08.07.2025, 0.5d
    Docker + CI/CD ergänzen      :a8, 09.07.2025, 1d
    Doku finalisieren + abgeben 🟦 :milestone, a8, 10.07.2025
```

### ✅ Stufe 2 – Schweizer Datumsformat + wöchentliche Gliederung
- Alle Daten sind im Format `DD.MM.YYYY`
- Die Abschnitte sind: Vorbereitung, Infrastruktur, Dienste & Sicherheit, Feinschliff

### ✅ Stufe 3 – Individuelle Farben & Meilensteine
- 🟩 für **Backups**
- 🟦 für **Abgabe**

---

_Fortsetzung folgt mit Aufgabe 2..._
