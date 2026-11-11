# Prüfablauf MVP v0.2: vom Modell zum Ergebnis

Wie die Prüfung funktioniert, woher die Werte kommen, aus welcher Tabelle und mit welchem Rechenweg.
Ausgeführt wird alles im Notebook `checks/Team2_U-Wert_Berechnung.ipynb`. Stand: 03.11.2026

```
1. Modell lesen               →  Welche Wände sind Aussenwände? Wie dick? Welche Materialien?
2. Aufbau zuordnen            →  checks/aufbau.csv: Dicke und λ pro Schicht
3. U-Wert rechnen             →  U = 1 / (Rsi + Σ d/λ + Rse)
4. Mit Grenzwert vergleichen  →  U ≤ 0.28?
5. Ins Modell schreiben und mit IDS prüfen
```

---

## Schritt 1: Was das Modell liefert

Quelle: `models/BIMcollab_Example_ARC.ifc` (IFC2X3, Längen in mm). Das Notebook liest pro Wand:

| Was | Wo im IFC | Beispiel |
|---|---|---|
| Ist es eine Aussenwand? | `Pset_WallCommon.IsExternal` | `TRUE` bei 70 von 171 Wänden |
| Wanddicke | `BaseQuantities.Width` (mm × 0.001 = m) | 340 mm |
| Materialien | Materialliste der Wand | Stone - limestone, Insulation - plastic hard, Air, Stone - brick |
| Wandfläche (nur Heizlast) | `BaseQuantities.NetSideArea` | in m² |

**Was das Modell nicht hat:** die Dicke jeder einzelnen Schicht und die λ-Werte. Darum braucht es Schritt 2.

Zusätzlich markiert das Notebook verdächtige Aussenwände: «internal» im Typnamen oder dünner als 15 cm (37 von 70 Wänden).

---

## Schritt 2: Der Aufbau (`checks/aufbau.csv`)

Eine Zeile pro Schicht, von innen nach aussen, mit Dicke `d_m`, Wärmeleitfähigkeit `lambda_W_mK` oder Widerstand `R_m2K_W`, Belüftung und Quelle.

**Schichtdicken (Annahme):** so gewählt, dass ihre Summe die Wanddicke im Modell ergibt (z.B. 100 + 100 + 40 + 100 = 340 mm). Beim Typ «pl-iso-hsb 10-38-140-12» stehen die Dicken im Namen (10 / 38 / 140 / 12 mm).

**λ-Werte:** Bemessungswerte der Wärmeleitfähigkeit nach **DIN 4108-4:2020-11**

| Material im Modell | Angenommen als | λ [W/(m·K)] | Tabelle |
|---|---|---|---|
| Stone - limestone | Kalksandstein, 1800 kg/m³ | 0.99 | DIN 4108-4, Tab. 1, Zeile 4.2 |
| Stone - brick | Klinker / Vollziegel, 1800 kg/m³ | 0.81 | DIN 4108-4, Tab. 1, Zeile 4.1.1 / 4.1.2 |
| Plaster inside | Gipsputz, 1000 kg/m³ | 0.34 | DIN 4108-4, Tab. 1, Zeile 1.1.2 |
| Insulation - plastic hard | EPS, λD 0.035 | 0.036 | DIN 4108-4, Tab. 2, Zeile 5.2 |
| Insulation - plastic soft | Mineralwolle, λD 0.035 | 0.036 | DIN 4108-4, Tab. 2, Zeile 5.1 |
| Reinforced concrete | Stahlbeton armiert (1 % Stahl), 2300 kg/m³ | 2.3 | DIN EN ISO 10456:2010-05, Tab. 3 |
| Wood plywood | Sperrholz, 500 kg/m³ | 0.13 | DIN EN ISO 10456:2010-05, Tab. 3 |

**Dämmstoffe:** Der Hersteller gibt einen Nennwert λD an (angenommen 0.035). Nach DIN 4108-4, Tab. 2, Fussnote a, gilt als Bemessungswert λB = λD × 1.03, mindestens λD + 0.001:
0.035 × 1.03 = 0.036

**Luftschichten** nach **DIN EN ISO 6946:2018-03**:

| Fall | Regel | Wert |
|---|---|---|
| ruhende Luftschicht ab 25 mm (6.9.2, Tabelle 8) | fester Widerstand R | 0.18 m²K/W |
| zweischaliges Mauerwerk mit offenen Stossfugen (6.9.2, Anmerkung) | Stossfugen gelten nicht als Lüftungsöffnungen → ruhend | 0.18 m²K/W |
| stark belüftete Luftschicht, hinterlüftete Fassade (6.9.4) | diese Luftschicht und alle Schichten weiter aussen werden **nicht gerechnet**, aussen gilt Rse = Rsi | Rse = 0.13 m²K/W |

Kavitätswand = ruhend (laut Norm). Annahme: Holzfassade (Timberframe) und Marmorplatte (Facade plating) = hinterlüftet.

---

## Schritt 3: Der Rechenweg (DIN EN ISO 6946:2018-03)

```
R   = d / λ                          Gleichung (3)
R_T = Rsi + R1 + R2 + … + Rn + Rse    Gleichung (4)
U   = 1 / R_T                        Gleichung (1)
```

Endergebnis U auf **zwei signifikante Stellen** runden (6.5.2): 0.169 → 0.17, 0.298 → 0.30. Der Vergleich mit dem Grenzwert nutzt den ungerundeten Wert.

| Grösse | Bedeutung | Wert |
|---|---|---|
| Rsi | Wärmeübergangswiderstand innen, waagrechter Wärmestrom (Wand), Tabelle 7 | 0.13 m²K/W |
| Rse | Wärmeübergangswiderstand aussen, Tabelle 7 | 0.04 m²K/W (hinterlüftet: 0.13, 6.9.4) |
| d | Schichtdicke | m |
| λ | Wärmeleitfähigkeit | W/(m·K) |
| d/λ | Wärmedurchlasswiderstand der Schicht | m²K/W |

### Beispiel 1: Timberframe internal wall - limestone (8 Wände), besteht

| Schicht | Rechnung | R [m²K/W] |
|---|---|---|
| Rsi | | 0.130 |
| Kalksandstein | 0.100 / 0.99 | 0.101 |
| EPS | 0.060 / 0.036 | 1.667 |
| Folie | vernachlässigt | 0.000 |
| Mineralwolle | 0.140 / 0.036 | 3.889 |
| Hinterlüftung + Holzschalung | nicht gerechnet | |
| Rse (hinterlüftet) | | 0.130 |
| **R_T** | | **5.917** |

U = 1 / 5.917 = **0.169 W/(m²K)** (gerundet 0.17) ≤ 0.28 → **bestanden**

Vereinfachung: Die Holzständer in der Dämmschicht sind nicht gerechnet. Nach DIN EN ISO 6946, 6.7.2, wäre das eine inhomogene Schicht (Mittel aus oberem und unterem Grenzwert); der echte U-Wert ist etwas höher.

### Beispiel 2: Cavity wall masonry-limestone (26 Wände), fällt durch

| Schicht | Rechnung | R [m²K/W] |
|---|---|---|
| Rsi | | 0.130 |
| Kalksandstein | 0.100 / 0.99 | 0.101 |
| EPS | 0.100 / 0.036 | 2.778 |
| Luftschicht 40 mm (ruhend) | Tabellenwert | 0.180 |
| Vormauerziegel | 0.100 / 0.81 | 0.123 |
| Rse | | 0.040 |
| **R_T** | | **3.352** |

U = 1 / 3.352 = **0.298 W/(m²K)** (gerundet 0.30) > 0.28 → **durchgefallen**

Empfindlichkeit: Mit einer Dämmung λ = 0.024 statt 0.036 (z.B. XPS oder PU mit λD 0.023, DIN 4108-4 Tab. 2 Z. 5.3 / 5.4) wäre U = 0.21 → bestanden. Die Wahl des Dämmstoffs entscheidet.

### Alle Wandtypen

Die vollständige Rechnung jedes Wandtyps steht in `results/rechnungen_wandtypen.md`.

| Wandtyp | Anzahl | U [W/(m²K)] | Ergebnis |
|---|---|---|---|
| Timberframe internal wall - limestone | 8 | 0.169 | bestanden |
| Cavity wall masonry-limestone | 26 | 0.298 | durchgefallen |
| Exterior wall, masonry + insulation 240mm | 2 | 0.308 | durchgefallen |
| pl-iso-hsb 10-38-140-12 200 | 4 | 0.655 | durchgefallen |
| Facade plating | 5 | 1.226 | durchgefallen |
| Reinforced concrete (LB) | 1 | 3.022 | durchgefallen |
| Stone - brick | 2 | 3.408 | durchgefallen |
| Limestone 100 | 22 | 3.690 | durchgefallen |

---

## Schritt 4: Vergleich mit dem Grenzwert

| | |
|---|---|
| **Grenzwert** | U ≤ **0.28 W/(m²K)** |
| **Quelle** | GEG (Gebäudeenergiegesetz), Anlage 1, Zeile 1.1: Aussenwand U = 0.28 W/(m²·K) |
| **Hinweis** | Wert des **Referenzgebäudes** für den Neubau-Nachweis, kein gesetzlicher Höchstwert für jede einzelne Wand. Wir benutzen ihn als Prüfwert. |

Zusätzliche Kontrollen im Notebook:
- Summe der Schichtdicken passt zur Wanddicke im Modell (± 5 mm)
- Hinweis «IsExternal prüfen» bei «internal» im Typnamen oder unter 15 cm Dicke

Ergebnis pro Wand: **bestanden**, **durchgefallen** oder **fehlend** (wenn der Aufbau unvollständig ist; fehlend zählt nie als bestanden).

---

## Schritt 5: Ins Modell schreiben und mit IDS prüfen

1. Das Notebook schreibt den berechneten U-Wert in eine **Kopie** des Modells: `Pset_WallCommon.ThermalTransmittance`. Das Original bleibt unverändert.
2. Die IDS-Regel `requirements/Team2_U-Wert_Aussenwand.ids`:
   - **Anwendungsbereich:** `IfcWall` mit `Pset_WallCommon.IsExternal = true`
   - **Anforderung:** `Pset_WallCommon.ThermalTransmittance` vorhanden und ≤ 0.28
3. ifctester prüft Original und Kopien. Gleiche Regel, nur die Daten ändern sich:

| Fall | Datei | IDS-Ergebnis |
|---|---|---|
| Ausgangslage | Original ohne U-Werte | 0 von 70 bestanden |
| positiv | Kopie mit U aus `aufbau.csv` | 8 von 70 bestanden |
| negativ | Kopie, Timberframe mit 40 mm statt 140 mm Mineralwolle (U = 0.319) | 0 von 70 bestanden |

4. Ergebnis pro Wand in `results/u_wert_aussenwaende.csv`: GlobalId, Objekt, Dicke, Ist-Wert U, Soll, Ergebnis, Grund.

---

## Zusatz: Bezug zu unserer Heizlast-Doku (DIN EN 12831)

Unsere Formel aus der Projektarbeit (TH Lübeck 2025), jetzt pro Aussenwand aus dem Modell:

```
Φ_T = A × (U + ΔU_TB) × f_x × Δθ
```

| Wert | Woher |
|---|---|
| A | `NetSideArea` aus dem Modell |
| U | berechnet in Schritt 3 |
| ΔU_TB = 0.10 W/(m²K) | DIN EN 12831 NA, Tabelle NA.2, Fall D |
| f_x = 1.0 | DIN EN 12831 NA, Tabelle NA.26, Aussenluft |
| Δθ = 20 − (−12) = 32 K | wie in unserer Beispielrechnung |

Ergebnis: Φ_T der Aussenwände ≈ **18.9 kW** (743 m² Wandfläche). Davon 9.3 kW auf die 22 verdächtigen «Limestone 100»-Wände.
ΔU_TB gehört nur zur Heizlast, nicht zur U-Wert-Prüfung.

---

## Was belegt ist und was Annahme

| Belegt (im Original nachgelesen) | Annahme (muss das Team prüfen) |
|---|---|
| Formeln, Rsi/Rse, Luftschichten, Belüftung, Runden (DIN EN ISO 6946:2018-03) | Dicke jeder Schicht |
| λ Kalksandstein, Ziegel, Gipsputz, Dämmstoffe (DIN 4108-4:2020-11) | welcher Dämmstoff (EPS / Mineralwolle, λD 0.035) |
| λ Stahlbeton, Sperrholz (DIN EN ISO 10456:2010-05) | Material «limestone» = Kalksandstein, Rohdichte 1800 |
| Kavitätswand ruhend (DIN EN ISO 6946, 6.9.2 Anmerkung) | Holzfassade und Marmor hinterlüftet |
| Grenzwert 0.28 (GEG Anlage 1, Gesetzestext online) | Holzständer nicht gerechnet (vereinfacht) |
| ΔU_TB, f_x, Δθ (unsere Heizlast-Doku) | |

## Quellen

- DIN EN ISO 6946:2018-03 (EN ISO 6946:2017), Tabelle 7, Tabelle 8, Abschnitte 6.5.2, 6.7.1, 6.7.2, 6.9.2 bis 6.9.4
- DIN 4108-4:2020-11, Tabelle 1 (Zeilen 1.1.2, 4.1.1, 4.1.2, 4.2) und Tabelle 2 (Zeilen 5.1 bis 5.4, Fussnote a)
- DIN EN ISO 10456:2010-05, Tabelle 3
- Normen über die Zentrale Hochschulbibliothek Lübeck, nachgelesen am 03.11.2026
- GEG Anlage 1: <https://www.gesetze-im-internet.de/geg/anlage_1.html>
- DIN EN 12831: unsere Projektarbeit «Heizlastberechnung eines würfelförmigen Wohngebäudes nach DIN EN 12831 mittels Python», TH Lübeck 2025
