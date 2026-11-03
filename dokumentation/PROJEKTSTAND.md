# Projektstand Team 2 · U-Wert der Gebäudehülle

BFH Minor BXMid03 «Data Management und BIM», HS 2026/27
Stand: **03.11.2026** · 

Diese Datei beantwortet drei Fragen: **Wo stehen wir? Was liegt wo? Was ist noch offen?**

---

## 1. Worum es geht (in 3 Sätzen)

Die Bauphysik braucht für den Energienachweis die U-Werte der Aussenwände. Heute fehlen sie im IFC-Modell, darum wird per Telefon nachgefragt und in Excel gerechnet.
Unser MVP berechnet den U-Wert aus dem Wandaufbau, schreibt ihn ins Modell und prüft ihn automatisch mit einer IDS-Regel.

**Soll-Prozess:** Bauphysik liefert Aufbau → U-Wert → Modell → IDS-Prüfung

---

## 2. Wo stehen wir? (Zeitachse)

| Datum | Meilenstein | Was wir abgegeben bzw. gemacht haben | Status |
|---|---|---|---|
| 12.10.2026 | AIA-BEP-Matrix | Matrix und IDS «Wandmengen» (andere Fragestellung, Kostenplanung) | abgegeben |
| 19.10.2026 | Prozessmodell | IST/SOLL-Prozess U-Wert (`workflow/Team_2_U-Wert_Prozess_Ist_Soll.drawio.pdf`) | abgegeben |
| 27.10.2026 | Kurs Automatisierung I | Auftrag MVP v0.1, Team-Repository | erledigt |
| 02.11.2026 | **MVP v0.1** | Prüfung «U-Wert vorhanden» mit IFC-Lite an einer Testwand, positiv und negativ | in unserer Kopie; Abgabe auf Moodle: _bitte bestätigen_ |
| 03.11.2026 | Feedback Dozent | Starter-Notebook und echtes Modell `BIMcollab_Example_ARC.ifc` per Pull Request in unsere Kopie, Vorschlag zur Vertiefung | übernommen |
| 03.11.2026 | **MVP v0.2** | U-Wert aus Aufbau berechnen, ins Modell schreiben, IDS ≤ 0.28, Negativfall, Heizlast-Bezug | **in Arbeit: Werte prüfen** |
| _offen_ | Peer-Audit / nächste Abgabe | _Datum eintragen_ | _offen_ |

---

## 3. Was liegt wo?

```
README.md                    Hauptbeschreibung MVP (Problem, Input, Verarbeitung, Output, Ausführen, Testfälle)
PROJEKTSTAND.md              diese Datei: Stand, Ablage, offene Punkte
KI_USAGE.md                  wo und wie wir KI eingesetzt haben

checks/
  Team2_U-Wert_Berechnung.ipynb   MVP v0.2: unser Notebook (in Colab ausführen)
  aufbau.csv                      Wandaufbau pro Wandtyp: d, λ, Quelle, Status  ← HIER arbeiten wir
  Team2_U-Wert_Starter.ipynb      Vorlage unseres Dozenten (nicht verändern)

models/
  BIMcollab_Example_ARC.ifc       echtes Architekturmodell, 70 Aussenwände, ohne U-Werte (v0.2)
  Team2_Wand_U_ok.ifc             Testwand mit U = 0.15 (v0.1, positiv)
  Team2_Wand_ohne_U.ifc           Testwand ohne U (v0.1, negativ)

requirements/
  anforderung.md                  Anforderung, Normen und Quellen
  Team2_U-Wert_Aussenwand.ids     Regel v0.2: Aussenwand, U ≤ 0.28 (vom Notebook erzeugt)
  Team2_U-Wert.ids / .yaml        Regel v0.1: U vorhanden (YAML nach Vorlage Dozent)

results/
  u_wert_aussenwaende.csv         Ergebnis v0.2 pro Wand
  u_wert_aussenwaende_negativfall.csv
  ergebnis.csv                    Ergebnis v0.1
  README.md                       Übersicht aller Läufe

workflow/
  prozess.md                      wo das MVP im Soll-Prozess steht
  Team_2_U-Wert_Prozess_Ist_Soll.drawio(.pdf)   Abgabe 19.10.

poster/                           noch leer (Vorlage Dozent)
```

**Wo liegt was online?**

| Was | Adresse |
|---|---|
| Team-Repository (offiziell, Abgabe-Link) | https://github.com/LTplus-AG/bxmid03-hs26-team-2 |
| unsere Kopie (hier arbeiten wir, weil wir im Team-Repo keine Schreibrechte haben) | https://github.com/puderzuckerimschnee-max/bxmid03-hs26-team-2 |
| Kursmaterial | https://github.com/LTplus-AG/bxmid03-hs26 |
| IFC-Lite (Prüfung im Browser) | https://www.ifclite.com |

---

## 4. Wie arbeiten wir? (Kurzanleitung)

**Notebook laufen lassen**
1. In unserer Kopie `checks/Team2_U-Wert_Berechnung.ipynb` öffnen
2. «In Colab öffnen» → «Laufzeit» → «Alle ausführen»
3. Ergebnis steht unten in Abschnitt 11

**Wandaufbau ändern**
1. `checks/aufbau.csv` herunterladen und in Excel öffnen (Trennzeichen Semikolon)
2. Werte prüfen oder ändern, jede Zahl mit Quelle, Spalte `Status` auf `geprüft`
3. Als CSV (UTF-8) speichern, im Ordner `checks` hochladen, Notebook neu laufen lassen

**Dateien hochladen**
- Immer zuerst in den richtigen Ordner klicken, dann «Add file → Upload files», dann «Commit changes»
- Nie mehrere Ordner auf einmal hineinziehen (der Browser löst die Ordner auf)
- Zum Schluss Pull Request an das Team-Repo: «Contribute → Open pull request»

**Regel: Daten ändern, Regel beibehalten.** Fällt eine Wand durch, wird der Aufbau oder das Modell korrigiert, nicht der Grenzwert.

---

## 5. Aktuelles Ergebnis (MVP v0.2, Lauf 03.11.2026)

| Fall | IDS-Ergebnis |
|---|---|
| Modell ohne U-Werte | 0 von 70 bestanden |
| positiv: U aus `aufbau.csv` | 8 von 70 bestanden (Timberframe, U = 0.169) |
| negativ: Timberframe mit 40 mm statt 140 mm Mineralwolle | 0 von 70 bestanden (U = 0.319) |

Grenzwert: U ≤ 0.28 W/(m²K), GEG Anlage 1 Zeile 1.1. Berechnung nach DIN EN ISO 6946, λ nach DIN 4108-4:2020-11.
Heizlast-Bezug (DIN EN 12831, wie in unserer Projektarbeit 2025): Φ_T der Aussenwände ca. 18.9 kW.

**Achtung:** Diese Zahlen beruhen auf dem **Vorschlag** in `aufbau.csv`. Ändern wir den Aufbau, ändert sich das Ergebnis.

---

## 6. Entscheidungen, die wir getroffen haben

| Datum | Entscheidung | Warum |
|---|---|---|
| 01.11. | Prüfung mit IFC-Lite statt eigenem Python-Skript (v0.1) | passt zu unserem Wissensstand, im Kurs gezeigt |
| 02.11. | Regel v0.1 nach YAML-Vorlage des Dozenten, nur «U vorhanden» | die Vorlage kennt kein Wort für Grenzwerte |
| 02.11. | Negativfall v0.1 = Wand ohne U-Wert | genau unsere Schwachstelle im IST-Prozess |
| 03.11. | v0.2 mit dem Notebook des Dozenten weiterführen | U-Wert kann automatisch ins Modell geschrieben werden |
| 03.11. | Normbasis Deutschland (DIN, GEG) | passt zu unserer Heizlast-Projektarbeit nach DIN EN 12831 |
| 03.11. | Aufbau als Vorschlag von KI, wir prüfen | Modell hat keine Schichtdicken und keine λ-Werte |

---

## 7. Offene Punkte (To-do)

| # | Aufgabe | Wer | Bis | Erledigt |
|---|---|---|---|---|
| 1 | `aufbau.csv` prüfen: Quellen öffnen, Werte kontrollieren, `Status` auf `geprüft` | _Name_ | _Datum_ | ☐ |
| 2 | Klären: Welcher Dämmstoff ist «Insulation - plastic hard» (EPS, XPS, PIR)? | _Name_ | | ☐ |
| 3 | λ für Stahlbeton und Sperrholz in DIN EN ISO 10456 nachschlagen | _Name_ | | ☐ |
| 4 | Grenzwert 0.28 selbst in GEG Anlage 1 nachlesen; Anlage 1 oder Anlage 7? | _Name_ | | ☐ |
| 5 | Luftschicht Kavitätsmauerwerk: ruhend oder belüftet? | _Name_ | | ☐ |
| 6 | Eine Wand selbst von Hand nachrechnen (z.B. Cavity wall) und im README ergänzen | _Name_ | | ☐ |
| 7 | 37 verdächtige Aussenwände: Befund für den Architekten formulieren (`IsExternal`) | _Name_ | | ☐ |
| 8 | `KI_USAGE.md` korrigieren («Grenzwerte selber ausgedacht» stimmt nicht mehr) und ergänzen | _Name_ | | ☐ |
| 9 | Notebook selbst einmal in Colab laufen lassen und Ergebnis vergleichen | _Name_ | | ☐ |
| 10 | Dateien v0.2 in unsere Kopie hochladen und Pull Request an das Team-Repo | _Name_ | | ☐ |
| 11 | Ausblick: Dach, Boden, Fenster; BCF-Befund automatisch erzeugen | | | ☐ |

---

## 8. Begriffe kurz erklärt

| Begriff | Bedeutung |
|---|---|
| **IFC** | offenes Dateiformat für BIM-Modelle |
| **IDS** | Datei mit Prüfregeln für IFC-Modelle («Information Delivery Specification») |
| **Pset / Property** | Eigenschaftensatz bzw. Eigenschaft eines Bauteils, z.B. `Pset_WallCommon.ThermalTransmittance` = U-Wert |
| **GlobalId** | eindeutige Kennung eines Bauteils, damit man es im Viewer wiederfindet |
| **U-Wert** | Wärmedurchgangskoeffizient in W/(m²K), je kleiner desto besser gedämmt |
| **λ (Lambda)** | Wärmeleitfähigkeit eines Baustoffs in W/(m·K) |
| **Rsi / Rse** | Wärmeübergangswiderstand innen / aussen |
| **Fork / Kopie** | unsere eigene Kopie des Team-Repos auf GitHub |
| **Commit** | gespeicherte Änderung auf GitHub |
| **Pull Request** | Vorschlag, unsere Änderungen ins Team-Repo zu übernehmen |
| **Colab** | Google-Dienst, um Notebooks im Browser auszuführen |

---

## 9. Wie läuft unser Modell bisher?

1. Modell lesen        →  Welche Wände sind Aussenwände? Wie dick? Welche Materialien?
2. Aufbau zuordnen     →  aufbau.csv: Dicke und λ pro Schicht
3. U-Wert rechnen      →  U = 1 / (Rsi + Σ d/λ + Rse)
4. Mit Grenzwert vergleichen  →  U ≤ 0.28?
5. Ins Modell schreiben und mit IDS prüfen

## Schritt 1: Was das Modell liefert
| Was | Wo im IFC | Beispiel |
|---|---|---|
|Ist es eine Aussenwand?|Pset_WallCommon.IsExternal|TRUE bei 70 von 171 Wänden|
|Wanddicke|BaseQuantities.Width (in mm, ×0.001 → m)|340 mm|
|Materialien|Materialliste der Wand|Stone - limestone, Insulation - plastic hard, Air, Stone - brick|
|Wandfläche|BaseQuantities.NetSideArea|in m²|
Was das Modell nicht hat: die Dicke jeder einzelnen Schicht und die λ-Werte. Darum braucht es Schritt 2.

## Schritt 2: Der Aufbau

**Schichtdicken (Annahme):** so gewählt, dass ihre Summe die Wanddicke im Modell ergibt (z.B. 100 + 100 + 40 + 100 = 340 mm). Beim Typ «pl-iso-hsb 10-38-140-12» stehen die Dicken im Namen (10 / 38 / 140 / 12 mm).

**λ-Werte:** Bemessungswerte der Wärmeleitfähigkeit nach **DIN 4108-4:2020-11**

| Material im Modell | Angenommen als | λ [W/(m·K)] | Tabelle |
|---|---|---|---|
| Stone - limestone | Kalksandstein, 1800 kg/m³ | 0.99 | DIN 4108-4, Tab. 1, Zeile 4.2 |
| Stone - brick | Klinker / Vollziegel, 1800 kg/m³ | 0.81 | DIN 4108-4, Tab. 1, Zeile 4.1.1 / 4.1.2 |
| Plaster inside | Gipsputz, 1000 kg/m³ | 0.34 | DIN 4108-4, Tab. 1, Zeile 1.1.2 |
| Insulation - plastic hard | EPS, λD 0.035 | 0.036 | DIN 4108-4, Tab. 2, Zeile 5.2 |
| Insulation - plastic soft | Mineralwolle, λD 0.035 | 0.036 | DIN 4108-4, Tab. 2, Zeile 5.1 |
| Reinforced concrete | Stahlbeton | 2.3 | **noch nicht belegt**: DIN EN ISO 10456 |
| Wood plywood | Sperrholz | 0.13 | **noch nicht belegt**: DIN EN ISO 10456 |

**Dämmstoffe:** Der Hersteller gibt einen Nennwert λD an (angenommen 0.035). Nach DIN 4108-4, Tab. 2, Fussnote a, gilt als Bemessungswert λB = λD × 1.03, mindestens λD + 0.001:
0.035 × 1.03 = 0.036

**Luftschichten** nach **DIN EN ISO 6946**:

| Fall | Regel | Wert |
|---|---|---|
| ruhende Luftschicht ab 25 mm (geschlossen) | fester Widerstand R | 0.18 m²K/W |
| stark belüftete Luftschicht (hinterlüftete Fassade) | diese Luftschicht und alle Schichten weiter aussen werden **nicht gerechnet**, aussen gilt Rse = Rsi | Rse = 0.13 m²K/W |

Annahme: Kavitätswand = ruhend; Holzfassade (Timberframe) und Marmorplatte (Facade plating) = hinterlüftet.

## Schritt 3: Der Rechenweg (DIN EN ISO 6946)

```
R_T = Rsi + d1/λ1 + d2/λ2 + … + Rse
U   = 1 / R_T
```

| Grösse | Bedeutung | Wert |
|---|---|---|
| Rsi | Wärmeübergangswiderstand innen, waagrechter Wärmestrom (Wand) | 0.13 m²K/W |
| Rse | Wärmeübergangswiderstand aussen | 0.04 m²K/W (hinterlüftet: 0.13) |
| d | Schichtdicke | m |
| λ | Wärmeleitfähigkeit | W/(m·K) |
| d/λ | Wärmedurchlasswiderstand der Schicht | m²K/W |

Beispiel 1: Timberframe internal wall - limestone (8 Wände), besteht

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

U = 1 / 5.917 = **0.169 W/(m²K)** ≤ 0.28 → **bestanden**

Beispiel 2: Cavity wall masonry-limestone (26 Wände), fällt durch

| Schicht | Rechnung | R [m²K/W] |
|---|---|---|
| Rsi | | 0.130 |
| Kalksandstein | 0.100 / 0.99 | 0.101 |
| EPS | 0.100 / 0.036 | 2.778 |
| Luftschicht 40 mm (ruhend) | Tabellenwert | 0.180 |
| Vormauerziegel | 0.100 / 0.81 | 0.123 |
| Rse | | 0.040 |
| **R_T** | | **3.352** |

U = 1 / 3.352 = **0.298 W/(m²K)** > 0.28 → **durchgefallen**

Empfindlichkeit: Mit einer Dämmung λ = 0.024 statt 0.036 wäre U = 0.21 → bestanden. Die Wahl des Dämmstoffs entscheidet.

Alle Wandtypen

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

## 10. Änderungsprotokoll dieser Datei

| Datum | Wer | Was |
|---|---|---|
| 03.11.2026 | _Name_ | Datei angelegt |
