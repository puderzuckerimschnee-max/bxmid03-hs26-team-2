# Modelle

| Datei | Zweck | U-Wert |
|---|---|---|
| `Team2_Wand_U_ok.ifc` | positiver Testfall | 0.15 W/(m²K) |
| `Team2_Wand_ohne_U.ifc` | negativer Testfall | fehlt |

**Herkunft:** Kursmodell `Demo_Holzrahmen_korrigiert.ifc`

**Was wir geändert haben:** Am Ende der Datei ein `Pset_WallCommon` an die
Wand gehängt. Im positiven Modell mit `ThermalTransmittance` (U-Wert 0.15),
im negativen Modell ohne `ThermalTransmittance`. Sonst nichts.

Der U-Wert 0.15 ist ein ausgedachter Testwert, um das Vorgehen zu simmulieren.

## Echtes Architekturmodell (Erweiterung MVP)

| Datei | Zweck |
|---|---|
| `BIMcollab_Example_ARC.ifc` | BIMcollab-Beispielmodell (Architektur), IFC2X3, Längen in mm. 171 Wände, davon 70 mit `Pset_WallCommon.IsExternal = TRUE`, **keine** mit U-Wert. Materialien als Liste ohne Schichtdicken. Verwendet in `checks/Team2_U-Wert_Starter.ipynb`. |
