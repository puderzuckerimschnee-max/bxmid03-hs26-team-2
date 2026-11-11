# Anforderung U-Wert Aussenwand

## MVP v0.2: U-Wert berechnen, ins Modell schreiben, prüfen

| | |
|---|---|
| **Was** | Jede Aussenwand hat einen U-Wert, und er hält den Grenzwert ein. |
| **Zweck** | Energienachweis für die Baueingabe, Grundlage für die Heizlast |
| **Objekte** | `IfcWall` mit `Pset_WallCommon.IsExternal = true` |
| **Datenpfad** | `Pset_WallCommon.ThermalTransmittance` |
| **Einheit** | W/(m²K) |
| **Regel** | vorhanden und ≤ 0.28 |
| **Wer liefert den Aufbau** | Bauphysik (`checks/aufbau.csv`) |
| **Wer schreibt den U-Wert ins Modell** | Notebook `checks/Team2_U-Wert_Berechnung.ipynb` (Kopie des Modells) |
| **Wer prüft** | Informationsmanagement (BIM-Koordinator AN) |
| **Wann** | nach Upload auf die CDE, Meilenstein Ende Phase 32 |
| **Regeldatei** | `Team2_U-Wert_Aussenwand.ids` (vom Notebook erzeugt) |

### Normen und Quellen

| Was | Wert | Quelle |
|---|---|---|
| Berechnungsverfahren | U = 1 / R_tot, R = d/λ, R_tot = Rsi + ΣR + Rse | DIN EN ISO 6946:2018-03, Gleichungen (1), (3), (4) |
| Wärmeübergang innen / aussen, horizontaler Wärmestrom | Rsi = 0.13, Rse = 0.04 m²K/W | DIN EN ISO 6946:2018-03, Tabelle 7 |
| ruhende Luftschicht ≥ 25 mm | R = 0.18 m²K/W | DIN EN ISO 6946:2018-03, 6.9.2 und Tabelle 8 |
| zweischaliges Mauerwerk mit offenen Stossfugen | Luftschicht gilt als ruhend | DIN EN ISO 6946:2018-03, 6.9.2 Anmerkung |
| stark belüftete Luftschicht | Luftschicht und äussere Schichten weglassen, Rse = Rsi | DIN EN ISO 6946:2018-03, 6.9.4 |
| Runden | U als Endergebnis auf zwei signifikante Stellen | DIN EN ISO 6946:2018-03, 6.5.2 |
| Kalksandstein 1800 kg/m³ | λ = 0.99 W/(m·K) | DIN 4108-4:2020-11 Tab. 1 Z. 4.2 |
| Vollziegel / Klinker 1800 kg/m³ | λ = 0.81 W/(m·K) | DIN 4108-4:2020-11 Tab. 1 Z. 4.1.1 / 4.1.2 |
| Gipsputz 1000 kg/m³ | λ = 0.34 W/(m·K) | DIN 4108-4:2020-11 Tab. 1 Z. 1.1.2 |
| EPS, Mineralwolle | λB = λD × 1.03 (λD 0.035 angenommen → 0.036) | DIN 4108-4:2020-11 Tab. 2 Z. 5.1 / 5.2, Fussnote a |
| Stahlbeton armiert 1 %, 2300 kg/m³ | λ = 2.3 W/(m·K) | DIN EN ISO 10456:2010-05 Tab. 3 |
| Sperrholz 500 kg/m³ | λ = 0.13 W/(m·K) | DIN EN ISO 10456:2010-05 Tab. 3 |
| Grenzwert Aussenwand | U ≤ 0.28 W/(m²K) | GEG Anlage 1, Zeile 1.1 (Referenzgebäude Wohngebäude) |
| Heizlast-Bezug | ΔU_TB = 0.10, f_x = 1.0, Δθ = 32 K | DIN EN 12831 NA, Tab. NA.2 und NA.26 (unsere Projektarbeit TH Lübeck 2025) |

Alle Normwerte am 03.11.2026 in den Originalnormen nachgelesen (DIN EN ISO 6946:2018-03, DIN 4108-4:2020-11, DIN EN ISO 10456:2010-05; Zugang über die Zentrale Hochschulbibliothek Lübeck). Übersicht: `requirements/tabellen_und_rechnungen.md`.
GEG Anlage 1: <https://www.gesetze-im-internet.de/geg/anlage_1.html>

## MVP v0.1: U-Wert vorhanden (weiterhin gültig)

| | |
|---|---|
| **Objekte** | `IfcWall` |
| **Datenpfad** | `Pset_WallCommon.ThermalTransmittance` |
| **Regel** | muss vorhanden sein |
| **Regeldateien** | `Team2_U-Wert.yaml` (Vorlage Dozent), `Team2_U-Wert.ids` (für IFC-Lite) |
