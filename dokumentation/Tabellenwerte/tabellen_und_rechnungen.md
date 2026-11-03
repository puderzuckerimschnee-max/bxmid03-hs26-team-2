# Tabellen und Rechnungen für die U-Wert-Berechnung

Übersicht, welche Normen, Tabellen und Rechenschritte das MVP v0.2 braucht und woher sie kommen.
Stand: 03.11.2026 · ☐ erst ankreuzen, wenn der Wert im **Original** nachgelesen ist.

**Legende Spalte «Quelle bei uns»**
- **PDF** = unsere Projektarbeit «Heizlastberechnung eines würfelförmigen Wohngebäudes nach DIN EN 12831 mittels Python», TH Lübeck 2025
- **Auszug** = von KI im Internet recherchiert (Auszug, nicht Originalnorm), Link unten
- **offen** = noch nachzuschlagen

---

## A. Tabellen

### 1. DIN EN ISO 6946: U-Wert-Berechnung

| ☐ | Tabelle | Werte | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | Wärmeübergangswiderstände | Rsi = 0.13, Rse = 0.04 m²K/W (horizontaler Wärmestrom = Wand) | Anfang und Ende jeder U-Wert-Rechnung | Auszug |
| ☐ | Wärmedurchlasswiderstand ruhender Luftschichten | 5 mm 0.11 · 7 mm 0.13 · 10 mm 0.15 · 15 mm 0.17 · ab 25 mm 0.18 m²K/W | R der Luftschichten | Auszug |
| ☐ | Abschnitt belüftete Luftschichten | ruhend / schwach belüftet (halber Wert) / stark belüftet (äussere Schichten weglassen, Rse = Rsi) | hinterlüftete Fassaden | Auszug |

Tabellennummern im Original nachschlagen (vermutlich Tabelle 7 und 8, nicht verifiziert).

### 2. DIN 4108-4:2020-11: λ-Werte (Bemessungswerte)

| ☐ | Tabelle / Zeile | Werte [W/(m·K)] | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | Tab. 1, Z. 4.2 Kalksandstein | 1800 kg/m³ → 0.99 · 2000 kg/m³ → 1.1 | Stone - limestone | Auszug |
| ☐ | Tab. 1, Z. 4.1.1 Klinker / Z. 4.1.2 Vollziegel | 1800 kg/m³ → 0.81 · 2000 kg/m³ → 0.96 | Stone - brick | Auszug |
| ☐ | Tab. 1, Z. 1.1.2 Gipsputzmörtel | 900 kg/m³ → 0.30 · 1000 kg/m³ → 0.34 | Plaster inside | Auszug |
| ☐ | Tab. 2, Z. 5.2 EPS | λB = λD × 1.03, mindestens λD + 0.001 | Insulation - plastic hard | Auszug |
| ☐ | Tab. 2, Z. 5.1 Mineralwolle | λB = λD × 1.03, mindestens λD + 0.001 | Insulation - plastic soft | Auszug |
| ☐ | Tab. 2, weitere Dämmstoffe (XPS, PUR/PIR) | falls «plastic hard» kein EPS ist | alternative Dämmung | offen |

### 3. DIN EN ISO 10456: λ-Werte, die in DIN 4108-4 fehlen

| ☐ | Material | Wert bisher | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | Stahlbeton (bewehrt) | 2.3 | Reinforced concrete | offen |
| ☐ | Sperrholz | 0.13 | Wood plywood | offen |
| ☐ | Nadelholz | wird nicht gerechnet (hinterlüftet) | Fassadenschalung | optional |
| ☐ | Marmor | wird nicht gerechnet (hinterlüftet) | Facade plating | optional |

### 4. GEG (Gebäudeenergiegesetz): Grenzwert

| ☐ | Stelle | Wert | Wofür | Quelle bei uns |
|---|---|---|---|---|
| ☐ | Anlage 1, Zeile 1.1 (Referenzgebäude Wohngebäude) | Aussenwand U = 0.28 W/(m²K) | Prüfwert in Notebook und IDS | Auszug (Gesetzestext online) |
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
| ☐ | 2. Bemessungswert Dämmung | λB = λD × 1.03 (mindestens λD + 0.001) | 0.035 → 0.036 | DIN 4108-4 | Auszug |
| ☐ | 3. Widerstand einer Schicht | R = d / λ | 0.100 / 0.99 = 0.101 m²K/W | DIN EN ISO 6946 | Auszug |
| ☐ | 4. Gesamtwiderstand | R_T = Rsi + Σ R + Rse | 0.13 + … + 0.04 | DIN EN ISO 6946 | Auszug |
| ☐ | 5. U-Wert | U = 1 / R_T | 1 / 3.352 = 0.298 W/(m²K) | DIN EN ISO 6946 | Auszug |
| ☐ | 6. Grenzwert-Vergleich | U ≤ 0.28 → bestanden, sonst durchgefallen | 0.298 > 0.28 → durchgefallen | GEG Anlage 1 | Auszug |
| ☐ | 7. Plausibilität Dicke | Σ d der Schichten = Wanddicke im Modell (± 5 mm) | 0.100 + 0.100 + 0.040 + 0.100 = 0.340 ✓ | | eigene Regel |
| ☐ | 8. Temperaturdifferenz | Δθ = θ_int − θ_e | 20 − (−12) = 32 K | DIN EN 12831 | PDF, Abschnitt 3 |
| ☐ | 9. Transmissionsverlust je Wand | Φ_T = A × (U + ΔU_TB) × f_x × Δθ | | DIN EN 12831, 8.3.2 | PDF, Abschnitt 3.4 |

---

## C. Eingaben, die nicht aus Tabellen kommen (Annahmen)

| ☐ | Was | Bisher angenommen | Wer klärt |
|---|---|---|---|
| ☐ | Dicke jeder Schicht | Summe = Wanddicke im Modell | Bauphysik / Team |
| ☐ | Dämmstoff und λD | EPS bzw. Mineralwolle, λD 0.035 | Team (Produktdatenblatt) |
| ☐ | Luftschicht ruhend oder belüftet | Kavitätswand ruhend, Holzfassade und Marmor hinterlüftet | Team |
| ☐ | «limestone» = Kalksandstein? | ja, Rohdichte 1800 kg/m³ | Team |

---

## D. Was in unserem PDF steht und was nicht

| Norm | Inhalt | Im PDF? |
|---|---|---|
| DIN EN 12831 | Tabellen NA.29, B.15, NA.2, NA.26, NA.27, B.14 und Formel Φ_T | ✅ ja |
| DIN EN ISO 6946 | Rsi, Rse, Luftschichten, Belüftung, U = 1 / R_T | ❌ nein |
| DIN 4108-4 | λ-Werte Kalksandstein, Ziegel, Putz, Dämmung | ❌ nein |
| DIN EN ISO 10456 | λ Stahlbeton, Sperrholz | ❌ nein |
| GEG | Grenzwert 0.28 | ❌ nein |

Für alles mit ❌ brauchen wir eigene Quellen, am besten die Originalnormen mit Ausgabe (z.B. über die Normendatenbank der Hochschule).

---

## Quellen

- DIN 4108-4:2020-11, Auszug: <https://www.hamburg.de/resource/blob/190582/4523febf3c69d9f64aa7f3d19b22721f/din4108-4-data.pdf>
- DIN EN ISO 6946, Auszug Rsi/Rse und Luftschichten: <https://www.delta-q.de/wp-content/uploads/beschreibung_bauliche_normen.pdf>
- GEG Anlage 1: <https://www.gesetze-im-internet.de/geg/anlage_1.html>
- DIN EN 12831: unsere Projektarbeit, TH Lübeck 2025 (Abb. 1 bis 5)
