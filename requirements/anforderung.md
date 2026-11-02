# Anforderung U-Wert Wand

| | |
|---|---|
| **Was** | Jede Wand hat einen U-Wert. |
| **Zweck** | Energienachweis für die Baueingabe |
| **Objekte** | `IfcWall` |
| **Datenpfad** | `Pset_WallCommon.ThermalTransmittance` |
| **Einheit** | W/(m²K) |
| **Regel** | muss vorhanden sein |
| **Wer liefert** | Architekt (Modellautor) |
| **Wer prüft** | Informationsmanagement (BIM-Koordinator AN) |
| **Wann** | nach Upload auf die CDE, Meilenstein Ende Phase 32 |
| **Regeldateien** | `Team2_U-Wert.yaml` (Vorlage Dozent), `Team2_U-Wert.ids` (für IFC-Lite) |

## Nächster Schritt: Grenzwert

Die Bauphysik prüft danach, ob der U-Wert den Grenzwert einhält:
0.17 W/(m²K) für Wand, Dach und Boden gegen aussen bei Neubauten
(Einzelbauteilnachweis, SIA 380/1, Ausgabe 2016).
