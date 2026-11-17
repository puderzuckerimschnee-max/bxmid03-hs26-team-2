# Team 2 · U-Wert der Gebäudehülle

BFH Minor BXMid03 «Data Management und BIM», HS 2026/27.
**MVP v0.2** · Stand 03.11.2026 (v0.1 siehe unten)

## Problem und Zielgruppe
**Wer:** Informationsmanagement (BIM-Koordinator AN), zusammen mit der Bauphysik.
**Welche Entscheidung:** Haben alle Aussenwände im IFC-Modell einen U-Wert, und hält er den Grenzwert ein? Ja: Modell geht an die Bauphysik für den Energienachweis. Nein: Befund mit GlobalId an den Architekten.
**Wann:** Nach dem Upload des IFC auf die CDE, Meilenstein Ende Phase 32, vor der Baueingabe.

Heute kommt das IFC **ohne U-Werte**. Die Bauphysik fragt per Telefon oder Mail nach und rechnet von Hand in Excel (siehe Prozessmodell IST/SOLL in `workflow/`).
**Neu in v0.2:** Fehlt der U-Wert, berechnen wir ihn aus dem Wandaufbau der Bauphysik, schreiben ihn ins Modell und prüfen ihn mit IDS. So wird unser Soll-Prozess umgesetzt: **Bauphysik liefert Aufbau → U-Wert → Modell → IDS.**

## Input
- **IFC-Modell:** `models/BIMcollab_Example_ARC.ifc`, IFC2X3, Längen in mm, BIMcollab-Beispielmodell (Architektur), bereitgestellt von unserem Dozenten (siehe `models/README.md`). 171 Wände, davon 70 mit `IsExternal = TRUE`, keine mit U-Wert.
- **Wandaufbau:** `checks/aufbau.csv`, eine Zeile pro Schicht mit Dicke d, λ bzw. R und Quelle. **Status: Vorschlag, von uns noch zu prüfen.**
- **Regel/Anforderung:** `requirements/anforderung.md`, IDS `requirements/Team2_U-Wert_Aussenwand.ids` (wird vom Notebook erzeugt).

## Verarbeitung
- **Scope:** `IfcWall` mit `Pset_WallCommon.IsExternal = true` (70 Wände)
- **Berechnung:** U = 1 / (Rsi + Σ d/λ + Rse) nach **DIN EN ISO 6946:2018-03** (Gleichungen 1, 3, 4), Rsi = 0.13, Rse = 0.04 m²K/W (Tabelle 7); ruhende Luftschicht 0.18 (Tabelle 8); hinterlüftete Fassaden: äussere Schichten weglassen, Rse = 0.13 (6.9.4)
- **λ-Werte:** **DIN 4108-4:2020-11** (Tabellen 1 und 2), Dämmstoffe λB = λD × 1.03; Stahlbeton und Sperrholz aus **DIN EN ISO 10456:2010-05** Tabelle 3. Alle Normwerte im Original geprüft, Übersicht in `requirements/tabellen_und_rechnungen.md`, Rechenweg in `workflow/pruefablauf.md`
- **Datenpfad:** U wird geschrieben nach `Pset_WallCommon.ThermalTransmittance`, Einheit W/(m²K), in eine **Kopie** des Modells
- **Regel:** U vorhanden und **≤ 0.28 W/(m²K)** (GEG Anlage 1, Zeile 1.1, Referenzwert Aussenwand)
- **Zusätzlich:** Hinweis bei verdächtigen Aussenwänden («internal» im Typnamen oder unter 15 cm dick) und Plausibilität Schichtdicken gegen Wanddicke im Modell

## Output
- `results/u_wert_aussenwaende.csv`: eine Zeile pro Aussenwand mit GlobalId, Objekt, Dicke, Ist-Wert (U berechnet), Soll-Wert, Ergebnis, Grund
- `results/u_wert_aussenwaende_negativfall.csv`: dasselbe für den Negativfall
- `requirements/Team2_U-Wert_Aussenwand.ids`: die Prüfregel, auch in IFC-Lite ladbar
- lokal (nicht im Repository, je ca. 18 MB): `BIMcollab_Example_ARC_mit_U.ifc` und `..._negativ.ifc`

## Setup
- **Variante A (empfohlen): Google Colab im Browser**, nichts installieren, Google-Konto nötig
- **Variante B: lokal** mit Python 3.12 und `pip install ifcopenshell==0.9.0.post1 ifctester==0.9.0 pandas`
- Notebook: `checks/Team2_U-Wert_Berechnung.ipynb` (weitergeführt aus dem Starter-Notebook unseres Dozenten)

## Ausführen
```
Variante A (Colab):
1. checks/Team2_U-Wert_Berechnung.ipynb auf GitHub öffnen
2. Oben auf «In Colab öffnen» klicken
3. Menü «Laufzeit» → «Alle ausführen» (beim ersten Mal «Trotzdem ausführen» bestätigen)
4. Modell und aufbau.csv werden automatisch von GitHub geladen
5. Ergebnis unten in Abschnitt 11 ablesen; CSV und IDS werden heruntergeladen

Variante B (lokal):
1. Repository herunterladen und in den Ordner checks/ wechseln
2. jupyter notebook Team2_U-Wert_Berechnung.ipynb
3. «Run All»; Ergebnisse landen in results/ und requirements/

Gegenprobe in IFC-Lite (nur die Regel, ohne Berechnung):
requirements/Team2_U-Wert_Aussenwand.ids zusammen mit der erzeugten Kopie
BIMcollab_Example_ARC_mit_U.ifc laden: Analyze → Data validation → Run Validation
```

## Testfälle
Gleiche Regel (IDS, Grenzwert 0.28), nur die Daten ändern sich. Lauf vom 03.11.2026 (IfcOpenShell 0.9.0, ifctester).

| Fall | Datei | Erwartet | Tatsächlich |
|---|---|---|---|
| Ausgangslage | `models/BIMcollab_Example_ARC.ifc` (ohne U) | 0 von 70 bestanden | 0 von 70 bestanden |
| positiv | Kopie mit U aus `aufbau.csv`; Wandtyp «Timberframe» U = 0.169 | Timberframe bestanden | 8 von 70 bestanden (alle 8 Timberframe-Wände) |
| negativ | gleiche Kopie, Timberframe mit 40 mm statt 140 mm Mineralwolle, U = 0.319 | Timberframe durchgefallen | 0 von 70 bestanden |

Ergebnis pro Wandtyp (positiver Fall):

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

Die Rechnung **aller 8 Wandtypen**, Schicht für Schicht mit Quelle: `results/rechnungen_wandtypen.md`.

### Handrechnung (Kontrolle des Codes)
Wandtyp «Timberframe internal wall - limestone», von innen nach aussen:

| Schicht | d [m] | λ [W/(m·K)] | R [m²K/W] | Quelle |
|---|---|---|---|---|
| Rsi | | | 0.130 | DIN EN ISO 6946 |
| Kalksandstein 1800 kg/m³ | 0.100 | 0.99 | 0.101 | DIN 4108-4 Tab. 1 Z. 4.2 |
| EPS, λD 0.035 | 0.060 | 0.036 | 1.667 | DIN 4108-4 Tab. 2 Z. 5.2 |
| Folie | 0 | | 0.000 | vernachlässigt |
| Mineralwolle, λD 0.035 | 0.140 | 0.036 | 3.889 | DIN 4108-4 Tab. 2 Z. 5.1 |
| Hinterlüftung + Holzschalung | | | nicht gerechnet | DIN EN ISO 6946, stark belüftet |
| Rse (= Rsi) | | | 0.130 | DIN EN ISO 6946 |
| **Summe** | | | **5.917** | |

U = 1 / 5.917 = **0.169 W/(m²K)** ≤ 0.28 → bestanden. Das Notebook rechnet denselben Wert (Abschnitt 5b).

### Bezug zu unserer Heizlast-Doku (DIN EN 12831)
Mit den berechneten U-Werten rechnet das Notebook wie in unserer Projektarbeit Φ_T = A × (U + ΔU_TB) × f_x × Δθ für jede Aussenwand (ΔU_TB = 0.10, f_x = 1.0, Δθ = 32 K, A = Netto-Wandfläche aus dem Modell): **Φ_T der Aussenwände ≈ 18.9 kW** bei 743 m² Wandfläche. Davon fallen 9.3 kW auf die 22 verdächtigen «Limestone 100»-Wände: Ein falsches `IsExternal` verfälscht also auch die Heizlast.

## Grenzen und offene Punkte
- **Die Aufbautabelle ist ein Vorschlag.** Das Modell kennt nur Materialnamen und Gesamtdicke. Schichtdicken sind so angenommen, dass sie die Wanddicke ergeben; die Dämmstoffe sind als EPS bzw. Mineralwolle mit λD 0.035 angenommen. Mit einem besseren Dämmstoff (z.B. λ = 0.024 statt 0.036) ergäbe die Cavity wall U = 0.21 und würde bestehen.
- **Luftschicht im Kavitätsmauerwerk:** gilt nach DIN EN ISO 6946, 6.9.2 Anmerkung, als ruhend (offene Stossfugen sind keine Lüftungsöffnungen).
- **Holzständer** in den Dämmschichten (Timberframe, pl-iso-hsb) sind nicht gerechnet. Genauer wäre die inhomogene Schicht nach DIN EN ISO 6946, 6.7.2; der U-Wert der Timberframe-Wand ist dadurch etwas zu günstig.
- U wird im Ergebnis zusätzlich auf zwei signifikante Stellen gerundet ausgegeben (Spalte `U_Angabe`, DIN EN ISO 6946, 6.5.2); der Grenzwert-Vergleich nutzt den ungerundeten Wert.
- **37 von 70 Aussenwänden sind verdächtig** (22 × «Limestone 100» mit 100 mm, 8 × «Timberframe *internal* wall», 5 × 50 mm «Facade plating», 2 × 100 mm Ziegel). Hier muss der Architekt `IsExternal` bzw. die Modellierung klären.
- **Grenzwert 0.28** ist der Referenzwert des GEG für den Neubau-Nachweis, kein fester Höchstwert pro Bauteil. Alternativ wäre GEG Anlage 7 (Höchstwerte bei Änderung bestehender Gebäude) möglich.
- Der U-Wert ohne Wärmebrücken wird geprüft; ΔU_TB (0.10) geht nur in die Heizlast ein.
- Lokal getestet mit IfcOpenShell 0.9.0 und ifctester aus dem IfcOpenShell-Repository; in Colab läuft die im Notebook angegebene Version 0.9.0.post1.
- Nur Wände; Dach, Boden, Fenster fehlen noch. BCF-Befund noch nicht automatisiert.

## MVP v0.1 (Einstieg, weiterhin gültig)
Prüfung «U-Wert vorhanden» mit IFC-Lite 5.3.1 im Browser an einer Testwand: `models/Team2_Wand_U_ok.ifc` (U = 0.15) → 1 passed, `models/Team2_Wand_ohne_U.ifc` (ohne U) → 1 failed, Regel `requirements/Team2_U-Wert.ids` bzw. `Team2_U-Wert.yaml`. Details in `results/README.md`.

## Team
Wer hat was beigetragen? (Commits zeigen es, hier kurz zusammenfassen)
| Person | Beitrag |
|---|---|
| Felix | zusammen gearbeitet|
| Lilly| zusammen gearbeitet |

Beim Erstellen hat uns KI geholfen, siehe `KI_USAGE.md`.
