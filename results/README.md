# Ergebnisse

## MVP v0.2 (03.11.2026)

**Lauf:** `checks/Team2_U-Wert_Berechnung.ipynb`, IfcOpenShell 0.9.0, ifctester; Modell `models/BIMcollab_Example_ARC.ifc`, Aufbau `checks/aufbau.csv` (Status Vorschlag), Regel `requirements/Team2_U-Wert_Aussenwand.ids` (U ≤ 0.28, GEG Anlage 1)

| Datei | Inhalt |
|---|---|
| `u_wert_aussenwaende.csv` | 70 Aussenwände: GlobalId, Objekt, Dicke, Ist-Wert U, Soll, Ergebnis, Grund |
| `rechnungen_wandtypen.md` | U-Wert-Rechnung aller 8 Wandtypen Schicht für Schicht, mit Quellen und Negativfall |
| `u_wert_aussenwaende_negativfall.csv` | dasselbe, Timberframe mit 40 mm statt 140 mm Mineralwolle |

| Fall | IDS-Ergebnis (ifctester) |
|---|---|
| Original ohne U-Werte | 0 von 70 bestanden |
| positiv: U aus Aufbau | 8 von 70 bestanden (alle Timberframe, U = 0.169) |
| negativ: dünnere Dämmung | 0 von 70 bestanden (Timberframe U = 0.319) |

### Gegenprobe in IFC-Lite (03.11.2026)

Regel `requirements/Team2_U-Wert_Aussenwand.ids` in IFC-Lite (Analyze → Data validation) auf das **Original** `models/BIMcollab_Example_ARC.ifc` angewendet:

| | IFC-Lite | Notebook (ifctester) |
|---|---|---|
| geprüfte Aussenwände | 70 | 70 |
| bestanden | 0 | 0 |
| Grund | «Property "ThermalTransmittance" not found in "Pset_WallCommon"» bei allen 70 | U fehlt |

Beide Werkzeuge stimmen überein. Bericht: `results/ifclite_bericht_original.html`. Für die Kopien mit U-Werten (`BIMcollab_Example_ARC_mit_U.ifc` → erwartet 8 von 70, `..._negativ.ifc` → erwartet 0 von 70) die Dateien aus Colab herunterladen und in IFC-Lite prüfen: _Ergebnis eintragen_.

## MVP v0.1 (02.11.2026)

| Datei | Inhalt |
|---|---|
| `ergebnis.csv` | Ergebnis beider Testfälle (GlobalId, Objekt, Ist-Wert, Soll-Wert, Ergebnis, Grund) |
| _Screenshots_ | _optional: je ein Screenshot pro Testfall_ |

**Lauf:** IFC-Lite 5.3.1, 02.11.2026, Analyze → Data validation → IDS validation,
Regel `requirements/Team2_U-Wert.ids` («Aussenwände U-Wert»)

| Fall | IFC-Lite zeigt |
|---|---|
| positiv (`Team2_Wand_U_ok.ifc`) | 1 entity · 1 passed · 0 failed · 1/1 checks passed (100%) |
| negativ (`Team2_Wand_ohne_U.ifc`) | 1 entity · 0 passed · 1 failed · 0/1 checks passed (0%) · Property "Pset_WallCommon.ThermalTransmittance" must exist |

In beiden Fällen ist es dieselbe Wand: `Wall #1`, IfcWall, GlobalId `2ucZRLBGP4uxZW$9i1VAZ8`.
