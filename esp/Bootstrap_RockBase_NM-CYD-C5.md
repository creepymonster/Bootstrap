# Universeller ESP-IDF-Projekt-Bootstrap

## 1. Rolle und Auftrag
Du bist ein erfahrener Embedded-Softwarearchitekt und ESP-IDF-Entwickler. Initialisiere ein neues oder bestehendes GitHub-Repository als sauberes, wartbares ESP-IDF-Projekt. Dieser Auftrag umfasst ausschließlich den Bootstrap, nicht die Implementierung der eigentlichen Projektfunktionen. Arbeite nur im angegebenen Zielrepository. Verweise nicht auf andere Projekt-Repositories als Strukturvorlage.

## 2. Projektangaben
- Zielrepository: `<GITHUB_REPOSITORY_URL>`
- Projektname: `<PROJECT_NAME>`
- Projektbeschreibung: `<PROJECT_DESCRIPTION>`
- Zusätzliche Hardware: `<OPTIONAL_HARDWARE>`
- Besondere Anforderungen: `<SPECIAL_REQUIREMENTS>`

Fehlende Angaben als offene Punkte dokumentieren, nicht erfinden.

## 3. Zielhardware und Referenzen
**Board:** RockBase NM-CYD-C5 mit ESP32-C5. **ESP-IDF-Target:** `esp32c5`.

**Hardwareprofil:** Integriertes ST7789-TFT (320 × 240 im Querformat), resistiver XPT2046-Single-Touch, nominell 16 MB Flash und 8 MB PSRAM; tatsächliche Bestückung prüfen. Eine microSD-Anbindung kann vorhanden sein, ihre Pins und Betriebsart müssen anhand der Boardrevision verifiziert werden. Display und Touch gehören zur Hardwaredokumentation, werden aber im Bootstrap noch nicht als Featuretreiber implementiert.

**Maßgebliche Referenzen:** Offizielle Espressif-ESP-IDF-Dokumentation für ESP32-C5 (`https://docs.espressif.com/projects/esp-idf/en/stable/esp32c5/`), verfügbare RockBase-NM-CYD-C5-Herstellerunterlagen und Schaltplan. Keine anderen Projekt-Repositories als Struktur- oder Codevorlage verwenden.

**Boardbesonderheiten:** RISC-V-Architektur, ESP32-C5-Funkfähigkeiten, Display-/Touch-SPI-Bus und mögliche microSD-Buskonflikte berücksichtigen. Keine GPIOs, PSRAM-Modi oder SD-Chip-Select-Werte ohne Quellennachweis festlegen.

## 4. Repository-Analyse
Prüfe zuerst vorhandene Dateien, Branch, Buildsystem und Dokumentation. Bei leerem Repository erstelle die Grundstruktur. Bei vorhandenem Code bewahre funktionierende Bestandteile, ergänze Fehlendes und vermeide destruktive Umstrukturierungen. Bei Konflikten zwischen Vorgaben und bestehendem Projekt dokumentiere die Abweichung.

## 5. Verbindliche Projektstruktur
```text
<PROJECT_NAME>/
├── .gitignore
├── README.md
├── AGENTS.md
├── CMakeLists.txt
├── sdkconfig.defaults
├── main/
│   ├── CMakeLists.txt
│   └── main.cpp
└── docs/
    ├── ARCHITECTURE.md
    ├── HARDWARE.md
    ├── TECHNICAL_TODOS.md
    ├── FEATURE_TODOS.md
    └── IDEAS.md
```
Diese fünf Dokumentationsdateien sind verpflichtend. Erstelle beim Bootstrap keine zusätzlichen Markdown-Dokumente. Kamera, Audio, Kommunikation, Speicherung, Sicherheit, Energieverwaltung und UI werden bei Relevanz zunächst als Abschnitte in `ARCHITECTURE.md` oder `HARDWARE.md` beschrieben. Keine leeren Komponentenverzeichnisse oder ungenutzten Treiber anlegen.

## 6. Minimales ESP-IDF-Projekt
- Verwende ESP-IDF mit C/C++, ohne Arduino-Abhängigkeiten.
- Wähle eine stabile, unterstützte ESP-IDF-Version und dokumentiere sie.
- Konfiguriere Zielchip, Flash, PSRAM und Partitionen passend zur tatsächlichen Hardware.
- Erstelle `app_main()` mit ESP-IDF-Logging, Projektname und Version, Chipinformationen, freiem Heap und einer Prüfung der PSRAM-Verfügbarkeit.
- Der Hauptablauf muss stabil und ressourcenschonend sein.
- Starte keine WLAN-, BLE- oder sonstigen Dienste ohne Projektanforderung.
- Erfinde keine Pinbelegungen, Hardwarefunktionen oder erfolgreichen Tests.

## 7. README.md
Verfasse die README auf Deutsch. Enthalten sein müssen Projektziel und Beschreibung, geplante und bereits implementierte Funktionen (klar getrennt), Hardware und Zusatzhardware, ESP-IDF-Version, Projektstruktur, Build-, Flash- und Monitor-Anleitung, Entwicklungsstand, bekannte Einschränkungen sowie Links auf die Dokumentation.

## 8. AGENTS.md
Erstelle verbindliche Regeln für zukünftige Coding-Agenten:
- Alle Markdown-Erklärtexte auf Deutsch; technische Symbole, APIs, Dateinamen, Konfigurationsschlüssel, Aufgaben-IDs und Commit-Nachrichten auf Englisch.
- ESP-IDF/C/C++, keine Arduino-Abhängigkeiten ohne ausdrückliche Freigabe.
- Nur im Zielrepository arbeiten; Hardwareannahmen und GPIOs verifizieren.
- Modulare, testbare Komponenten; Speicher, Task-Stacks, Queues und Laufzeiten begrenzen.
- Fehlerfälle behandeln, Zugangsdaten und Build-Artefakte nicht committen.
- Bestehenden funktionierenden Code erhalten.
- Architekturentscheidungen, Tests, Risiken und Aufgabenstatus aktuell dokumentieren.
- Kleine nachvollziehbare Commits mit englischen Nachrichten.
- Kennungen dauerhaft und fortlaufend führen; erledigte Einträge markieren statt löschen.
- Keine eigentlichen Projektfeatures ohne gesonderten Entwicklungsauftrag implementieren.

## 9. docs/ARCHITECTURE.md
Dokumentiere Projektziel, Systemübersicht, geplante Module und Abhängigkeiten, Datenfluss, ESP-IDF-/FreeRTOS-Konzept soweit erforderlich, Speicher- und Fehlerbehandlung, Energieaspekte soweit relevant, Teststrategie, Risiken und offene Entscheidungen. Verwende bei Bedarf Mermaid-Diagramme. Keine nicht beschlossenen Funktionen als feste Architektur darstellen.

## 10. docs/HARDWARE.md
Dokumentiere genaue Boardvariante und Revision, Chip, Flash/PSRAM, Spannungsversorgung, USB/Debug, GPIO und Schnittstellen, Boot-/Strapping-Pins, angeschlossene Peripherie, Pin-Konflikte und offene Hardwarefragen. Kennzeichne Aussagen als **Bestätigt**, **Geplant** oder **Ungeklärt**. Technische Werte anhand der maßgeblichen Hardwarequellen verifizieren.

## 11. docs/TECHNICAL_TODOS.md
Verwende eine Tabelle mit `Kennung | Status | Aufgabe | Abnahmekriterium`. Kennungen beginnen mit `TECH-0001` und sind dauerhaft eindeutig. Status: `Offen`, `In Arbeit`, `Erledigt`, `Blockiert`. Erfasse relevante Bootstrap-, Build-, Speicher-, GPIO-, Debug-, Test- und CI-Aufgaben; keine künstlichen Einträge.

## 12. docs/FEATURE_TODOS.md
Verwende eine Tabelle mit `Kennung | Status | Funktion | Abnahmekriterium`. Kennungen beginnen mit `FEAT-0001`. Features nur aus der Projektbeschreibung ableiten. Falls keine Funktionen feststehen, die leere Liste mit erklärendem Platzhalter dokumentieren; keine Features erfinden.

## 13. docs/IDEAS.md
Verwende eine Tabelle mit `Kennung | Idee | Hinweise`. Kennungen beginnen mit `IDEA-0001`. Ideen sind unverbindlich und keine beschlossenen Anforderungen. Ohne passende Ideen bleibt eine dokumentierte leere Liste bestehen.

## 14. Speicher, Komponenten und Erweiterbarkeit
Prüfe Flash-Größe, PSRAM-Typ, internen und DMA-fähigen RAM, NVS und Partitionstabelle. OTA nur bei Bedarf vorsehen. Künftige Komponenten können unter `components/` entstehen, werden aber im Bootstrap nicht als leere Platzhalter erzeugt. Vermeide unnötige Abhängigkeiten.

## 15. Build und Verifikation
Führe nach Möglichkeit aus:
```bash
idf.py set-target esp32c5
idf.py build
```
Prüfe Zielplattform, Warnungen, Flash-/PSRAM-Einstellungen und Abhängigkeiten. Wenn geeignete Hardware vorhanden und ein Flash-Test erlaubt ist, verwende `idf.py -p <PORT> flash monitor`. Kennzeichne nicht durchgeführte Hardwaretests ausdrücklich. Ein erfolgreicher Build beweist keine funktionierende Peripherie.

## 16. Grenzen des Auftrags
Erlaubt: Grundstruktur, minimale Startfirmware, Board-/Buildkonfiguration, README, AGENTS.md, fünf verpflichtende Dokumentationsdateien, Aufgabenlisten und verfügbare Buildtests. Nicht erlaubt: eigentliche Projektfeatures, ungefragte Netzwerkdienste, Display-, Touch-, Kamera-, Audio- oder SD-Treiber, zusätzliche Dokumentationsdateien, große Beispieldaten oder unnötige Bibliotheken.

## 17. Git-Arbeitsweise
Analysiere das Repository, erstelle den Bootstrap, führe verfügbare Tests aus, prüfe Änderungen und committe sie in kleinen Schritten mit englischen Commit-Nachrichten. Pushe auf den vorgesehenen Branch, sofern Schreibzugriff besteht. Bei fehlendem Zugriff den Zustand dokumentieren und keinen Push behaupten. Keine Referenzrepositories verändern.

## 18. Abschlussprüfung und Ergebnisbericht
Kontrolliere Zielchip, Hardwarekonfiguration, alle Pflichtdateien, deutsche Dokumentation, eindeutige Aufgabenkennungen, fehlende unnötige Treiber und Buildstatus. Berichte Repository-Link, Boardvariante, ESP-IDF-Version, Flash/PSRAM, angelegte Dateien, Testergebnisse, offene Fragen, nicht durchgeführte Hardwaretests und Commit-Referenzen. Beende danach die Arbeit; keine eigenständige Featureentwicklung.

**Beginne jetzt mit Repository- und Hardwareanalyse und führe anschließend den Bootstrap vollständig aus.**
