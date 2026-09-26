# Fussbodenheizung-Raspberry

Lokale Steuerung einer elektrischen Fußbodenheizung mit Raspberry Pi Zero 2 W, AZ-Touch Pi0, MLX90614/GY-906, Shelly 1 Mini Gen3 und Home Assistant.

## Ziel

Der Raspberry übernimmt die lokale Thermostatlogik und Bedienung. Der Shelly schaltet die 230-V-Heizung. Home Assistant dient für Visualisierung, Sollwerte, Automationen und optional die Fensterlogik.

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

## Geplante Funktionen

- Bodentemperatur per MLX90614/GY-906
- AZ-Touch-Oberfläche im Querformat 320 × 240
- Solltemperatur per Touch
- lokale Regelung mit Hysterese
- Shelly 1 Mini Gen3 lokal per WLAN schalten
- Home-Assistant-Anbindung per MQTT
- Fensterkontakt aus Home Assistant berücksichtigen
- Modi: Auto, Aus, Boost
- Sicherheitsabschaltung bei Sensorfehler
- Wiederanlauf nach Neustart
- systemd-Service
- Konfiguration über Datei

## Sicherheitsprinzip

Die Heizung soll auch ohne Home Assistant weiter geregelt werden. Home Assistant liefert optionale Zusatzinformationen und Bedienung, ist aber nicht die alleinige Regelinstanz.

Bei Sensorfehler oder ungültigen Messwerten wird die Heizung abgeschaltet.

> Arbeiten an 230 V dürfen nur fachgerecht und mit geeigneter Absicherung ausgeführt werden.

## Hardware

- Raspberry Pi Zero 2 W
- AZ-Touch Pi0, 2,8", 240 × 320
- MLX90614 / GY-906 IR-Temperatursensor
- Shelly 1 Mini Gen3
- elektrische Fußbodenheizung, ca. 500 W

## Status

Projektstart / Grundarchitektur festgelegt.
