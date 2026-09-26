# Roadmap

## Phase 1 – Hardware-Basis

- [ ] I²C am Raspberry aktivieren
- [ ] MLX90614/GY-906 anschließen
- [ ] Sensor unter Adresse 0x5A erkennen
- [ ] Temperatur zuverlässig auslesen
- [ ] AZ-Touch im Querformat 320 × 240 betreiben

## Phase 2 – Shelly

- [ ] feste IP/DHCP-Reservierung
- [ ] Shelly lokal per HTTP schalten
- [ ] Status zurücklesen
- [ ] Fehlerbehandlung bei Nichterreichbarkeit

## Phase 3 – Thermostat

- [ ] Sollwert
- [ ] Hysterese
- [ ] Mindest-Ein-/Ausschaltzeit
- [ ] Maximaltemperatur
- [ ] Sensorfehler-Sicherheitsabschaltung
- [ ] Auto / Aus / Boost

## Phase 4 – Display

- [ ] Isttemperatur
- [ ] Solltemperatur
- [ ] Plus/Minus
- [ ] Heizstatus
- [ ] Fensterstatus
- [ ] Betriebsmodus
- [ ] Fehlermeldungen

## Phase 5 – Home Assistant

- [ ] MQTT
- [ ] Climate-Entität
- [ ] Fensterstatus empfangen
- [ ] Sollwert synchronisieren
- [ ] Availability
- [ ] Discovery optional

## Phase 6 – Betrieb

- [ ] systemd-Service
- [ ] Logging
- [ ] Installationsskript
- [ ] Updateverfahren
- [ ] Dokumentation
