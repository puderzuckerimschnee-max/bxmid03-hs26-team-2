# Modelle

| Datei | Zweck | U-Wert |
|---|---|---|
| `Team2_Wand_U_ok.ifc` | positiver Testfall | 0.15 W/(m²K) |
| `Team2_Wand_ohne_U.ifc` | negativer Testfall | fehlt |

**Herkunft:** Kursmodell `Demo_Holzrahmen_korrigiert.ifc` (Kursrepository
`LTplus-AG/bxmid03-hs26`, Ordner `modelle/`), IFC4, eine Wand.

**Was wir geändert haben:** Am Ende der Datei ein `Pset_WallCommon` an die
Wand gehängt. Im positiven Modell mit `ThermalTransmittance` (U-Wert 0.15),
im negativen Modell ohne `ThermalTransmittance`. Sonst nichts.

Der U-Wert 0.15 ist ein **ausgedachter Testwert**, nicht berechnet.
