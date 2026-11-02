# Ergebnisse

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
