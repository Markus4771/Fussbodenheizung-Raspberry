# Architektur

## Regelprinzip

Der Raspberry ist die zentrale lokale Regelinstanz.

Prioritäten:

1. Sicherheitsabschaltung
2. Fenster offen
3. Manuell AUS
4. Boost
5. normale Temperaturregelung

## Temperaturregelung

Beispiel:

- Solltemperatur: 24,0 °C
- Hysterese: 0,4 °C
- EIN unter 23,6 °C
- AUS über 24,4 °C

Die Werte werden später konfigurierbar.

## Fensterlogik

Der Fensterstatus kann optional aus Home Assistant übernommen werden.

- Fenster offen → Heizung AUS
- Fenster geschlossen → Wiederanlauf nach konfigurierbarer Verzögerung
- Fensterfunktion kann deaktiviert werden
- optional Öffnungsverzögerung gegen kurzes Lüften

## Home Assistant

Kommunikation bevorzugt über MQTT.

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

## Shelly

Der Shelly 1 Mini Gen3 wird lokal im LAN angesprochen. Cloud-Abhängigkeit ist nicht vorgesehen.

## Fehlerfälle

- MLX90614 nicht erreichbar → Heizung AUS
- Temperatur außerhalb plausibler Grenzen → Heizung AUS
- MQTT/Home Assistant nicht erreichbar → lokale Regelung läuft weiter
- Shelly nicht erreichbar → Fehlerstatus auf Display und in MQTT
