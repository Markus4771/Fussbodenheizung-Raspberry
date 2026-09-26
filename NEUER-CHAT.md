# NEUER-CHAT.md

## Projekt

**Fussbodenheizung-Raspberry**

Ziel ist eine lokale, robuste Steuerung einer elektrischen Fußbodenheizung mit Raspberry Pi Zero 2 W und AZ-Touch Pi0. Die Heizung wird über einen Shelly 1 Mini Gen3 geschaltet. Home Assistant wird angebunden, soll aber nicht die alleinige Regelinstanz sein.

## Aktueller Hardwarestand

- Raspberry Pi Zero 2 W
- AZ-Touch Pi0 mit 2,8"-TFT
- Display-Auflösung: 240 × 320
- gewünschte Darstellung: Querformat 320 × 240
- MLX90614 / GY-906 IR-Temperatursensor vorhanden
- Shelly 1 Mini Gen3 für das Schalten der elektrischen Fußbodenheizung
- elektrische Fußbodenheizung ca. 500 W
- Raspberry und AZ-Touch funktionieren bereits grundsätzlich

## Architektur

```text
MLX90614 / GY-906
      │ I²C
      ▼
Raspberry Pi Zero 2 W
+ AZ-Touch Pi0
      │
      ├── lokale Thermostatregelung
      ├── Display / Touch
      ├── MQTT ↔ Home Assistant
      │
      └── WLAN / HTTP → Shelly 1 Mini Gen3
                              │
                              ▼
                    elektrische Fußbodenheizung
```

## Regelungsprinzip

Der Raspberry übernimmt die eigentliche lokale Regelung.

Beispiel:

- Solltemperatur: 24,0 °C
- Hysterese: 0,4 °C
- unter 23,6 °C → Heizung EIN
- über 24,4 °C → Heizung AUS

Geplant sind zusätzlich:

- Mindest-Einschaltdauer
- Mindest-Ausschaltdauer
- maximale Bodentemperatur
- Sicherheitsabschaltung bei Sensorfehler
- Modus Auto
- Modus Aus
- Modus Boost

## Fensterlogik

Die Fenstersteuerung ist optional und soll über Home Assistant eingebunden werden.

Geplante Priorität:

1. Sicherheitsabschaltung
2. Fenster offen
3. Manuell AUS
4. Boost
5. normale Temperaturregelung

Verhalten:

- Fenster offen → Heizung AUS
- optional Öffnungsverzögerung
- Fenster wieder geschlossen → Wiederanlauf nach konfigurierbarer Verzögerung
- Fensterfunktion kann deaktiviert werden

## Home Assistant

Home Assistant soll über MQTT angebunden werden.

Geplante Topics:

```text
fussbodenheizung/bad/temperature
fussbodenheizung/bad/target_temperature
fussbodenheizung/bad/heating
fussbodenheizung/bad/mode
fussbodenheizung/bad/window
fussbodenheizung/bad/availability

fussbodenheizung/bad/target_temperature/set
fussbodenheizung/bad/mode/set
```

Später soll eine Climate-/Thermostat-Entität in Home Assistant entstehen.

Wichtig: Fällt Home Assistant oder MQTT aus, soll die lokale Heizungsregelung auf dem Raspberry weiterlaufen.

## Shelly

Verwendet wird:

**Shelly 1 Mini Gen3**

Der Shelly soll lokal im LAN angesprochen werden. Eine Cloud-Abhängigkeit ist nicht vorgesehen.

Der Raspberry gibt dem Shelly abhängig von der Temperatur EIN-/AUS-Befehle.

## Temperatursensor

Vorhanden:

**MLX90614 / GY-906**

Geplanter Anschluss:

```text
GY-906       Raspberry Pi Zero 2 W

VCC   ─────► 3,3 V
GND   ─────► GND
SDA   ─────► GPIO 2 / Pin 3
SCL   ─────► GPIO 3 / Pin 5
```

Typische I²C-Adresse:

```text
0x5A
```

Vor dem Anschluss bzw. der finalen Verdrahtung muss geprüft werden, ob die benötigten I²C-Pins durch das AZ-Touch frei nutzbar sind.

## Display

Geplant ist eine Touch-Oberfläche im Querformat 320 × 240.

Darstellung:

- Isttemperatur
- Solltemperatur
- Plus-/Minus-Tasten
- Heizstatus EIN/AUS
- Fensterstatus
- Betriebsmodus
- Fehlermeldungen
- später optional weitere Einstellungen

## Sicherheitsprinzip

- Sensorfehler → Heizung AUS
- unplausible Temperatur → Heizung AUS
- maximale Bodentemperatur → Heizung AUS
- Home Assistant nicht erreichbar → lokale Regelung läuft weiter
- MQTT nicht erreichbar → lokale Regelung läuft weiter
- Shelly nicht erreichbar → Fehler anzeigen und protokollieren

Arbeiten an 230 V müssen fachgerecht und mit geeigneter Absicherung erfolgen.

## Bereits angelegte Dateien

- `README.md`
- `docs/ARCHITEKTUR.md`
- `docs/ROADMAP.md`
- `config.example.yaml`
- `NEUER-CHAT.md`

## Aktueller Entwicklungsstand

Projektgrundstruktur ist angelegt.

Die eigentliche Software für Sensor, Display, Shelly und MQTT wurde noch nicht umgesetzt.

## Nächster Schritt

**Phase 1 – Hardware-Basis**

1. I²C am Raspberry aktivieren
2. MLX90614/GY-906 anschließen
3. mit `i2cdetect -y 1` prüfen, ob Adresse `0x5A` erscheint
4. Temperatur auslesen
5. AZ-Touch im Querformat 320 × 240 betreiben
6. Temperatur auf dem Display darstellen

Danach:

- Shelly lokal ansteuern
- Thermostatlogik entwickeln
- Touch-Oberfläche erstellen
- MQTT/Home Assistant anbinden
- Fensterlogik ergänzen
- systemd-Service und Installationsskript erstellen

## Fortsetzung in einem neuen Chat

Zum Weiterarbeiten kann der neue Chat mit folgendem Auftrag gestartet werden:

> Lies bitte die Datei `NEUER-CHAT.md` aus meinem GitHub-Projekt `Fussbodenheizung-Raspberry` und führe die Entwicklung ab dem dort dokumentierten Stand weiter.
