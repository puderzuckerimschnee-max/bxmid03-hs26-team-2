# Rechnungen U-Wert für alle Wandtypen

Modell `models/BIMcollab_Example_ARC.ifc` (identisch mit `02_BIMcollab_Example_ARC_4.ifc`), Aufbau `checks/aufbau.csv`, Stand 03.11.2026.
Diese Datei wurde aus `aufbau.csv` erzeugt und stimmt mit dem Notebook überein.

**Rechenweg** nach DIN EN ISO 6946:2018-03:

```
R   = d / λ                          Gleichung (3)
R_T = Rsi + R1 + R2 + … + Rn + Rse    Gleichung (4)
U   = 1 / R_T                        Gleichung (1)
```

- Rsi = 0.13, Rse = 0.04 m²K/W (Tabelle 7, horizontaler Wärmestrom)
- ruhende Luftschicht ab 25 mm: R = 0.18 m²K/W (6.9.2, Tabelle 8)
- stark belüftete Luftschicht: diese und alle Schichten weiter aussen weglassen, Rse = Rsi = 0.13 (6.9.4)
- U als Endergebnis auf zwei signifikante Stellen runden (6.5.2)
- Grenzwert: U ≤ 0.28 W/(m²K), GEG Anlage 1, Zeile 1.1

Schichten jeweils **von innen nach aussen**. λ-Quellen in der Spalte «Quelle».

## Übersicht

| Wandtyp | Anzahl | Dicke Modell | R_T [m²K/W] | U [W/(m²K)] | U gerundet | Ergebnis |
|---|---|---|---|---|---|---|
| Cavity wall masonry-limestone | 26 | 0.340 m | 3.352 | 0.298 | 0.30 | durchgefallen |
| Limestone 100 | 22 | 0.100 m | 0.271 | 3.690 | 3.7 | durchgefallen |
| Timberframe internal wall - limestone | 8 | 0.365 m | 5.917 | 0.169 | 0.17 | bestanden |
| Facade plating | 5 | 0.050 m | 0.816 | 1.226 | 1.2 | durchgefallen |
| Exterior wall, masonry + insulation 240mm | 2 | 0.240 m | 3.251 | 0.308 | 0.31 | durchgefallen |
| pl-iso-hsb 10-38-140-12 200 | 4 | 0.200 m | 1.527 | 0.655 | 0.66 | durchgefallen |
| Stone - brick | 2 | 0.100 m | 0.293 | 3.408 | 3.4 | durchgefallen |
| Reinforced concrete (LB) | 1 | 0.370 m | 0.331 | 3.022 | 3.0 | durchgefallen |

Summe: 8 Aussenwände bestanden (Timberframe), 62 durchgefallen. IDS-Prüfung der Modellkopie: 8 von 70 bestanden.

## Cavity wall masonry-limestone

26 Aussenwände im Modell, Wanddicke im Modell 0.340 m, Summe Schichten 0.340 m ✓

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] | Quelle |
|---|---|---|---|---|---|
| Rsi | | | | 0.130 | DIN EN ISO 6946, Tab. 7 |
| Kalksandstein, Rohdichte 1800 kg/m³ | 0.100 | 0.99 | 0.100 / 0.99 | 0.101 | DIN 4108-4:2020-11 Tab. 1 Z. 4.2 (1800 kg/m³ → 0.99) |
| EPS-Hartschaum, λD 0.035 (Annahme) | 0.100 | 0.036 | 0.100 / 0.036 | 2.778 | DIN 4108-4:2020-11 Tab. 2 Z. 5.2 und Fussnote a (λB = λD × 1.03 → 0.036) |
| ruhende Luftschicht 40 mm (zweischaliges Mauerwerk, offene Stossfugen gelten nicht als Lüftung: 6.9.2 Anmerkung) | 0.040 | | Tabellenwert | 0.180 | DIN EN ISO 6946:2018-03 Abschn. 6.9.2 und Tab. 8 (horizontal, ab 25 mm → 0.18) |
| Vormauerziegel/Klinker, Rohdichte 1800 kg/m³ | 0.100 | 0.81 | 0.100 / 0.81 | 0.123 | DIN 4108-4:2020-11 Tab. 1 Z. 4.1.1 (1800 kg/m³ → 0.81) |
| Rse | | | | 0.040 | DIN EN ISO 6946, Tab. 7 |
| **R_T** | **0.340** | | | **3.352** | |

U = 1 / 3.352 = **0.298 W/(m²K)**, gerundet **0.30** → > 0.28 → **durchgefallen**

## Limestone 100

22 Aussenwände im Modell, Wanddicke im Modell 0.100 m, Summe Schichten 0.100 m ✓

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] | Quelle |
|---|---|---|---|---|---|
| Rsi | | | | 0.130 | DIN EN ISO 6946, Tab. 7 |
| Kalksandstein, Rohdichte 1800 kg/m³ | 0.100 | 0.99 | 0.100 / 0.99 | 0.101 | DIN 4108-4:2020-11 Tab. 1 Z. 4.2 (1800 kg/m³ → 0.99) |
| Rse | | | | 0.040 | DIN EN ISO 6946, Tab. 7 |
| **R_T** | **0.100** | | | **0.271** | |

U = 1 / 0.271 = **3.690 W/(m²K)**, gerundet **3.7** → > 0.28 → **durchgefallen**

## Timberframe internal wall - limestone

8 Aussenwände im Modell, Wanddicke im Modell 0.365 m, Summe Schichten 0.365 m ✓

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] | Quelle |
|---|---|---|---|---|---|
| Rsi | | | | 0.130 | DIN EN ISO 6946, Tab. 7 |
| Kalksandstein, Rohdichte 1800 kg/m³ | 0.100 | 0.99 | 0.100 / 0.99 | 0.101 | DIN 4108-4:2020-11 Tab. 1 Z. 4.2 (1800 kg/m³ → 0.99) |
| EPS-Hartschaum, λD 0.035 (Annahme) | 0.060 | 0.036 | 0.060 / 0.036 | 1.667 | DIN 4108-4:2020-11 Tab. 2 Z. 5.2 und Fussnote a (λB = λD × 1.03 → 0.036) |
| Folie, Dicke vernachlässigbar | 0.000 | | Tabellenwert | 0.000 | vernachlässigt (R ca. 0) |
| Mineralwolle, λD 0.035 (Annahme) | 0.140 | 0.036 | 0.140 / 0.036 | 3.889 | DIN 4108-4:2020-11 Tab. 2 Z. 5.1 und Fussnote a (λB = λD × 1.03 → 0.036) |
| Hinterlüftung 40 mm | 0.040 | | | nicht gerechnet | DIN EN ISO 6946:2018-03 Abschn. 6.9.4 (stark belüftet: Schichten ab hier weglassen, Rse = Rsi) |
| Holzschalung (wird nicht gerechnet) | 0.025 | | | nicht gerechnet | liegt vor der Hinterlüftung |
| Rse (= Rsi, hinterlüftet) | | | | 0.130 | DIN EN ISO 6946, 6.9.4 |
| **R_T** | **0.365** | | | **5.917** | |

U = 1 / 5.917 = **0.169 W/(m²K)**, gerundet **0.17** → ≤ 0.28 → **bestanden**

## Facade plating

5 Aussenwände im Modell, Wanddicke im Modell 0.050 m, Summe Schichten 0.050 m ✓

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] | Quelle |
|---|---|---|---|---|---|
| Rsi | | | | 0.130 | DIN EN ISO 6946, Tab. 7 |
| EPS-Hartschaum, λD 0.035 (Annahme) | 0.020 | 0.036 | 0.020 / 0.036 | 0.556 | DIN 4108-4:2020-11 Tab. 2 Z. 5.2 und Fussnote a (λB = λD × 1.03 → 0.036) |
| Hinterlüftung 10 mm | 0.010 | | | nicht gerechnet | DIN EN ISO 6946:2018-03 Abschn. 6.9.4 (stark belüftet: Schichten ab hier weglassen, Rse = Rsi) |
| Marmorplatte (wird nicht gerechnet) | 0.020 | | | nicht gerechnet | liegt vor der Hinterlüftung |
| Rse (= Rsi, hinterlüftet) | | | | 0.130 | DIN EN ISO 6946, 6.9.4 |
| **R_T** | **0.050** | | | **0.816** | |

U = 1 / 0.816 = **1.226 W/(m²K)**, gerundet **1.2** → > 0.28 → **durchgefallen**

## Exterior wall, masonry + insulation 240mm

2 Aussenwände im Modell, Wanddicke im Modell 0.240 m, Summe Schichten 0.240 m ✓

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] | Quelle |
|---|---|---|---|---|---|
| Rsi | | | | 0.130 | DIN EN ISO 6946, Tab. 7 |
| EPS-Hartschaum, λD 0.035 (Annahme) | 0.100 | 0.036 | 0.100 / 0.036 | 2.778 | DIN 4108-4:2020-11 Tab. 2 Z. 5.2 und Fussnote a (λB = λD × 1.03 → 0.036) |
| ruhende Luftschicht 40 mm (Annahme: nicht belüftet) | 0.040 | | Tabellenwert | 0.180 | DIN EN ISO 6946:2018-03 Abschn. 6.9.2 und Tab. 8 (horizontal, ab 25 mm → 0.18) |
| Vormauerziegel/Klinker, Rohdichte 1800 kg/m³ | 0.100 | 0.81 | 0.100 / 0.81 | 0.123 | DIN 4108-4:2020-11 Tab. 1 Z. 4.1.1 (1800 kg/m³ → 0.81) |
| Rse | | | | 0.040 | DIN EN ISO 6946, Tab. 7 |
| **R_T** | **0.240** | | | **3.251** | |

U = 1 / 3.251 = **0.308 W/(m²K)**, gerundet **0.31** → > 0.28 → **durchgefallen**

## pl-iso-hsb 10-38-140-12 200

4 Aussenwände im Modell, Wanddicke im Modell 0.200 m, Summe Schichten 0.200 m ✓

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] | Quelle |
|---|---|---|---|---|---|
| Rsi | | | | 0.130 | DIN EN ISO 6946, Tab. 7 |
| Gipsputz, Rohdichte 1000 kg/m³ | 0.010 | 0.34 | 0.010 / 0.34 | 0.029 | DIN 4108-4:2020-11 Tab. 1 Z. 1.1.2 (1000 kg/m³ → 0.34) |
| EPS-Hartschaum, λD 0.035 (Annahme) | 0.038 | 0.036 | 0.038 / 0.036 | 1.056 | DIN 4108-4:2020-11 Tab. 2 Z. 5.2 und Fussnote a (λB = λD × 1.03 → 0.036) |
| Ständerfeld 140 mm laut Modell ohne Dämmung, ruhend | 0.140 | | Tabellenwert | 0.180 | DIN EN ISO 6946:2018-03 Abschn. 6.9.2 und Tab. 8 (horizontal, ab 25 mm → 0.18) |
| Sperrholz | 0.012 | 0.13 | 0.012 / 0.13 | 0.092 | DIN EN ISO 10456:2010-05 Tab. 3, Sperrholz 500 kg/m³ → 0.13 |
| Rse | | | | 0.040 | DIN EN ISO 6946, Tab. 7 |
| **R_T** | **0.200** | | | **1.527** | |

U = 1 / 1.527 = **0.655 W/(m²K)**, gerundet **0.66** → > 0.28 → **durchgefallen**

## Stone - brick

2 Aussenwände im Modell, Wanddicke im Modell 0.100 m, Summe Schichten 0.100 m ✓

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] | Quelle |
|---|---|---|---|---|---|
| Rsi | | | | 0.130 | DIN EN ISO 6946, Tab. 7 |
| Vollziegel, Rohdichte 1800 kg/m³ | 0.100 | 0.81 | 0.100 / 0.81 | 0.123 | DIN 4108-4:2020-11 Tab. 1 Z. 4.1.2 (1800 kg/m³ → 0.81) |
| Rse | | | | 0.040 | DIN EN ISO 6946, Tab. 7 |
| **R_T** | **0.100** | | | **0.293** | |

U = 1 / 0.293 = **3.408 W/(m²K)**, gerundet **3.4** → > 0.28 → **durchgefallen**

## Reinforced concrete (LB)

1 Aussenwände im Modell, Wanddicke im Modell 0.370 m, Summe Schichten 0.370 m ✓

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] | Quelle |
|---|---|---|---|---|---|
| Rsi | | | | 0.130 | DIN EN ISO 6946, Tab. 7 |
| Stahlbeton | 0.370 | 2.3 | 0.370 / 2.3 | 0.161 | DIN EN ISO 10456:2010-05 Tab. 3, Beton armiert 1 % Stahl, 2300 kg/m³ → 2.3 |
| Rse | | | | 0.040 | DIN EN ISO 6946, Tab. 7 |
| **R_T** | **0.370** | | | **0.331** | |

U = 1 / 0.331 = **3.022 W/(m²K)**, gerundet **3.0** → > 0.28 → **durchgefallen**

## Negativfall: Timberframe mit dünnerer Dämmung

Gleiche Regel, nur die Mineralwolle ist 0.040 m statt 0.140 m dick.

| Schicht | d [m] | λ [W/(m·K)] | Rechnung | R [m²K/W] |
|---|---|---|---|---|
| Rsi | | | | 0.130 |
| Kalksandstein | 0.100 | 0.99 | 0.100 / 0.99 | 0.101 |
| EPS | 0.060 | 0.036 | 0.060 / 0.036 | 1.667 |
| Folie | 0.000 | | | 0.000 |
| Mineralwolle | **0.040** | 0.036 | 0.040 / 0.036 | 1.111 |
| Hinterlüftung + Holzschalung | | | | nicht gerechnet |
| Rse (= Rsi) | | | | 0.130 |
| **R_T** | | | | **3.139** |

U = 1 / 3.139 = **0.319 W/(m²K)**, gerundet **0.32** → > 0.28 → **durchgefallen**. IDS-Prüfung der Negativ-Kopie: 0 von 70 bestanden.

## Hinweise

- Die Schichtdicken sind angenommen (Summe = Wanddicke im Modell), die Dämmstoffe als EPS bzw. Mineralwolle mit λD 0.035. Siehe `requirements/tabellen_und_rechnungen.md`, Abschnitt C.
- Holzständer in den Dämmschichten sind nicht gerechnet (inhomogene Schicht nach DIN EN ISO 6946, 6.7.2). Die U-Werte von Timberframe und pl-iso-hsb sind dadurch etwas zu günstig.
- Der Vergleich mit dem Grenzwert nutzt den ungerundeten U-Wert.
