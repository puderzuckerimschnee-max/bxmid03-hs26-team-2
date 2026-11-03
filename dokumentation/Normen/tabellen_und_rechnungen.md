# Tabellen und Rechnungen für die U-Wert-Berechnung

Übersicht, welche Normen, Tabellen und Rechenschritte das MVP v0.2 braucht und woher sie kommen.
Stand: 03.11.2026 · **Im Original geprüft** = Wert in der Originalnorm (Zugang Zentrale Hochschulbibliothek Lübeck) nachgelesen.

**Legende Spalte «Quelle bei uns»**
- **Original ✓** = in der Originalnorm nachgelesen, Ausgabe angegeben
- **PDF** = unsere Projektarbeit «Heizlastberechnung eines würfelförmigen Wohngebäudes nach DIN EN 12831 mittels Python», TH Lübeck 2025
- **Gesetz online ✓** = Gesetzestext auf gesetze-im-internet.de gelesen
- **offen** = noch zu klären

---

## A. Tabellen

### 1. DIN EN ISO 6946:2018-03 (EN ISO 6946:2017): U-Wert-Berechnung

| ☐ | Stelle | Werte | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | Tabelle 7 · Konventionelle Wärmeübergangswiderstände | horizontal: Rsi = 0.13, Rse = 0.04 m²K/W | Anfang und Ende jeder U-Wert-Rechnung | Original ✓ |
| ☐ | Abschnitt 6.9.2 und Tabelle 8 · Ruhende Luftschichten | horizontal: 5 mm 0.11 · 7 mm 0.13 · 10 mm 0.15 · 15 mm 0.17 · 25 bis 300 mm 0.18 m²K/W (Zwischenwerte linear interpolieren) | R der Luftschichten | Original ✓ |
| ☐ | Abschnitt 6.9.2, Anmerkung | offene Stossfugen in der Aussenschale von zweischaligem Mauerwerk gelten **nicht** als Lüftungsöffnungen → Luftschicht ruhend | Cavity wall | Original ✓ |
| ☐ | Abschnitt 6.9.3 · Schwach belüftete Luftschicht | Öffnungen > 500 bis < 1500 mm² je m Länge; R_tot nach Gleichung (11) zwischen ruhend und stark belüftet interpolieren | wird bei uns nicht gebraucht | Original ✓ |
| ☐ | Abschnitt 6.9.4 · Stark belüftete Luftschicht | Öffnungen ≥ 1500 mm² je m Länge: Luftschicht und alle Schichten nach aussen weglassen, Rse = Rsi aus Tabelle 7 | hinterlüftete Fassaden | Original ✓ |
| ☐ | Abschnitt 6.7.2 · Inhomogene Schichten | oberer und unterer Grenzwert, Mittelwert (z.B. Holzständer in Dämmung) | **noch nicht umgesetzt** | Original ✓ |

### 2. DIN 4108-4:2020-11: λ-Werte (Bemessungswerte)

| ☐ | Tabelle / Zeile | Werte [W/(m·K)] | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | Tab. 1, Z. 4.2 Mauerwerk aus Kalksandsteinen | 1800 kg/m³ → 0.99 · 2000 kg/m³ → 1.1 | Stone - limestone | Original ✓ |
| ☐ | Tab. 1, Z. 4.1.1 Vollklinker | 1800 kg/m³ → 0.81 · 2000 kg/m³ → 0.96 | Stone - brick (Vormauerschale) | Original ✓ |
| ☐ | Tab. 1, Z. 4.1.2 Vollziegel | 1800 kg/m³ → 0.81 · 2000 kg/m³ → 0.96 | Stone - brick | Original ✓ |
| ☐ | Tab. 1, Z. 1.1.2 Gipsputzmörtel | 900 kg/m³ → 0.30 · 1000 kg/m³ → 0.34 | Plaster inside | Original ✓ |
| ☐ | Tab. 2, Z. 5.2 EPS + Fussnote a | λB = λD × 1.03, mindestens + 0.001 → λD 0.035 ergibt 0.036 | Insulation - plastic hard | Original ✓ |
| ☐ | Tab. 2, Z. 5.1 Mineralwolle + Fussnote a | wie EPS → 0.036 | Insulation - plastic soft | Original ✓ |
| ☐ | Tab. 2, Z. 5.3 XPS / Z. 5.4 PU | z.B. λD 0.023 → 0.024 | falls «plastic hard» kein EPS ist | Original ✓ |

### 3. DIN EN ISO 10456:2010-05: λ-Werte, die in DIN 4108-4 fehlen

| ☐ | Tabelle / Zeile | Werte [W/(m·K)] | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | Tab. 3, Beton armiert (mit 1 % Stahl) | 2300 kg/m³ → 2.3 | Reinforced concrete | Original ✓ |
| ☐ | Tab. 3, Sperrholz | 500 kg/m³ → 0.13 | Wood plywood | Original ✓ |
| ☐ | Tab. 3, Nutzholz | 450 kg/m³ → 0.12 | Holzständer (falls inhomogen gerechnet) | Original ✓ |
| ☐ | Tab. 3, Marmor | 2800 kg/m³ → 3.5 | wird nicht gerechnet (hinterlüftet) | Original ✓ |

### 4. GEG (Gebäudeenergiegesetz): Grenzwert

| ☐ | Stelle | Wert | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | Anlage 1, Zeile 1.1 (Referenzgebäude Wohngebäude) | Aussenwand U = 0.28 W/(m²K) | Prüfwert in Notebook und IDS | Gesetz online ✓ |
| ☐ | Anlage 7 (Höchstwerte bei Änderung bestehender Gebäude) | zum Vergleich nachlesen | Entscheid, welcher Wert besser passt | offen |

### 5. DIN EN 12831 (Beiblatt NA): Heizlast

| ☐ | Tabelle | Werte | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | NA.2 Wärmebrückenzuschlag | Fall D «alle anderen Fälle»: ΔU_TB = 0.10 W/(m²K) | Heizlast | PDF, Abb. 3 |
| ☐ | NA.26 Temperaturanpassungsfaktor | Aussenluft f_x = 1.0 · Erdreich 0.3 · unbeheizt 0.5 | Heizlast | PDF, Abb. 4 |
| ☐ | B.14 Norm-Innentemperatur | θ_int = 20 °C | Heizlast | PDF, erwähnt ohne Abbildung |
| ☐ | NA.29 Klimadaten | θ_e je nach Ort, bei uns −12 °C | Heizlast | PDF, Abb. 1 |
| ☐ | NA.27 Luftwechsel | nur für Lüftungswärmeverlust | Heizlast (optional) | PDF, Abb. 5 |
| ☐ | B.15 U-Werte nach Baujahr | nur als Notlösung, wenn kein Aufbau bekannt ist | optional | PDF, Abb. 2 |

---

## B. Rechnungen

| ☐ | Rechnung | Formel | Beispiel | Norm | Quelle bei uns |
|---|---|---|---|---|---|
| ☐ | 1. Einheit umrechnen | d [m] = Wanddicke im Modell [mm] × 0.001 | 340 mm → 0.340 m | | Modell |
| ☐ | 2. Bemessungswert Dämmung | λB = λD × 1.03 (mindestens λD + 0.001) | 0.035 → 0.036 | DIN 4108-4, Tab. 2, Fussnote a | Original ✓ |
| ☐ | 3. Widerstand einer Schicht | R = d / λ | 0.100 / 0.99 = 0.101 m²K/W | DIN EN ISO 6946, Gleichung (3) | Original ✓ |
| ☐ | 4. Gesamtwiderstand | R_tot = Rsi + R1 + … + Rn + Rse | 0.13 + … + 0.04 | DIN EN ISO 6946, Gleichung (4) | Original ✓ |
| ☐ | 5. U-Wert | U = 1 / R_tot | 1 / 3.352 = 0.298 W/(m²K) | DIN EN ISO 6946, Gleichung (1) | Original ✓ |
| ☐ | 6. Runden | Endergebnis U auf zwei signifikante Stellen | 0.298 → 0.30 · 0.169 → 0.17 | DIN EN ISO 6946, 6.5.2 | Original ✓ |
| ☐ | 7. Grenzwert-Vergleich | U ≤ 0.28 → bestanden, sonst durchgefallen | 0.298 > 0.28 → durchgefallen | GEG Anlage 1 | Gesetz online ✓ |
| ☐ | 8. Plausibilität Dicke | Σ d der Schichten = Wanddicke im Modell (± 5 mm) | 0.100 + 0.100 + 0.040 + 0.100 = 0.340 ✓ | | eigene Regel |
| ☐ | 9. Temperaturdifferenz | Δθ = θ_int − θ_e | 20 − (−12) = 32 K | DIN EN 12831 | PDF, Abschnitt 3 |
| ☐ | 10. Transmissionsverlust je Wand | Φ_T = A × (U + ΔU_TB) × f_x × Δθ | | DIN EN 12831, 8.3.2 | PDF, Abschnitt 3.4 |

---

## C. Eingaben, die nicht aus Tabellen kommen (Annahmen)

| ☐ | Was | Bisher angenommen | Wer klärt |
|---|---|---|---|
| ☐ | Dicke jeder Schicht | Summe = Wanddicke im Modell | Bauphysik / Team |
| ☐ | Dämmstoff und λD | EPS bzw. Mineralwolle, λD 0.035 | Team (Produktdatenblatt) |
| ☐ | Holzfassade und Marmor hinterlüftet (stark belüftet)? | ja | Team |
| ☐ | «limestone» = Kalksandstein, «brick» = Klinker / Vollziegel? | ja, Rohdichte 1800 kg/m³ | Team |
| ☐ | Holzständer in den Dämmschichten (Timberframe, pl-iso-hsb) | nicht gerechnet (U dadurch etwas zu günstig) | Team: inhomogen nach 6.7.2 rechnen? |

Die Luftschicht der Cavity wall ist **keine** Annahme mehr: Nach DIN EN ISO 6946, 6.9.2, Anmerkung gilt sie als ruhend.

---

## D. Was in unserem PDF steht und was nicht

| Norm | Inhalt | Im PDF? | Quelle |
|---|---|---|---|
| DIN EN 12831 | Tabellen NA.29, B.15, NA.2, NA.26, NA.27, B.14 und Formel Φ_T | ✅ ja | PDF |
| DIN EN ISO 6946:2018-03 | Rsi, Rse, Luftschichten, Belüftung, U = 1 / R_tot | ❌ nein | Originalnorm ✓ |
| DIN 4108-4:2020-11 | λ-Werte Kalksandstein, Ziegel, Putz, Dämmung | ❌ nein | Originalnorm ✓ |
| DIN EN ISO 10456:2010-05 | λ Stahlbeton, Sperrholz, Holz, Marmor | ❌ nein | Originalnorm ✓ |
| GEG | Grenzwert 0.28 | ❌ nein | Gesetzestext online ✓ |

---

## Quellen

- DIN EN ISO 6946:2018-03, Bauteile, Wärmedurchlasswiderstand und Wärmedurchgangskoeffizient, Berechnungsverfahren (EN ISO 6946:2017). Beuth, über Zentrale Hochschulbibliothek Lübeck
- DIN 4108-4:2020-11, Wärmeschutz und Energie-Einsparung in Gebäuden, Teil 4: Wärme- und feuchteschutztechnische Bemessungswerte. Beuth, über Zentrale Hochschulbibliothek Lübeck
- DIN EN ISO 10456:2010-05, Baustoffe und Bauprodukte, Wärme- und feuchtetechnische Eigenschaften, tabellierte Bemessungswerte. Beuth, über Zentrale Hochschulbibliothek Lübeck
- GEG Anlage 1: <https://www.gesetze-im-internet.de/geg/anlage_1.html>
- DIN EN 12831: unsere Projektarbeit, TH Lübeck 2025 (Abb. 1 bis 5)
