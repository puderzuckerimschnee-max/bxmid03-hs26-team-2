# Team 2 · U-Wert der Gebäudehülle

BFH Minor BXMid03 «Data Management und BIM», HS 2026/27.

## Problem und Zielgruppe
**Wer:** Informationsmanagement (BIM-Koordinator AN).
**Welche Entscheidung:** Hat jede Wand im IFC-Modell einen U-Wert? Ja: Modell geht an die Bauphysik für den Energienachweis. Nein: Modell geht mit Befund zurück an den Architekten.
**Wann:** Nach dem Upload des IFC auf die CDE, Meilenstein Ende Phase 32, vor der Baueingabe.
Heute kommt das IFC ohne U-Werte, die Bauphysik muss per Telefon oder Mail nachfragen und von Hand in Excel rechnen (siehe Prozessmodell IST/SOLL in `workflow/`).


## Input
- IFC-Modell: `models/Team2_Wand_U_ok.ifc` (positiv) und `models/Team2_Wand_ohne_U.ifc` (negativ), IFC4, abgeleitet vom Kursmodell `Demo_Holzrahmen_korrigiert.ifc` aus `LTplus-AG/bxmid03-hs26` (siehe `models/README.md`)
- Regel/Anforderung: `requirements/Team2_U-Wert.yaml` (IDS-Light, Vorlage Dozent), `requirements/Team2_U-Wert.ids` (IDS 1.0 für IFC-Lite), `requirements/anforderung.md`

## Verarbeitung
- **Scope:** alle Wände (`IfcWall`)
- **Datenpfad:** `Pset_WallCommon.ThermalTransmittance`, Einheit W/(m²K)
- **Regel:** U-Wert muss vorhanden sein (`presence: required`)

## Output
Das Ergebnis liegt in `results/ergebnis.csv`. Jede Zeile: GlobalId, Objekt, Ist-Wert, Soll-Wert, Ergebnis, Grund. In `results/README.md` steht, was IFC-Lite angezeigt hat.

## Setup
- Browser Chrome oder Edge
- IFC-Lite 5.3.1 im Browser: https://www.ifclite.com (Version steht unten rechts)
- Nichts installieren, das Modell bleibt auf dem eigenen Computer

## Ausführen
```
1. Repository herunterladen: GitHub → grüner Button «Code» → «Download ZIP» → entpacken
2. https://www.ifclite.com öffnen
3. «Open model file» → models/Team2_Wand_U_ok.ifc wählen
4. Menü «Analyze» → «Data validation» → Reiter «IDS validation»
5. «Load IDS File» → requirements/Team2_U-Wert.ids wählen
   (es muss «Document is valid — no audit issues» erscheinen)
6. «Run Validation» klicken
7. Ergebnis ablesen: 1 entity · 1 passed · 0 failed
8. Ordnersymbol oben links → models/Team2_Wand_ohne_U.ifc laden
9. «Analyze» → «Data validation» → «Run Validation»
10. Ergebnis ablesen: 1 entity · 0 passed · 1 failed
    Klick auf die Regel zeigt den Grund:
    Property "Pset_WallCommon.ThermalTransmittance" must exist
```

## Testfälle
| Fall | Datei | Erwartet | Tatsächlich |
|---|---|---|---|
| positiv | `models/Team2_Wand_U_ok.ifc` (U = 0.15 W/(m²K)) | bestanden | bestanden: 1 entity, 1 passed, 0 failed |
| negativ | `models/Team2_Wand_ohne_U.ifc` (U fehlt) | durchgefallen | durchgefallen: 1 entity, 0 passed, 1 failed, «must exist» |


## Grenzen und offene Punkte
- Geprüft wird nur, ob ein U-Wert vorhanden ist, nicht ob er richtig berechnet ist oder den Grenzwert einhält.
- Geprüft werden alle Wände, auch Innenwände. Für echte Projekte müssen Aussen- und Innenwände unterschieden werden.
- Nur Wände, Dach, Boden und Fenster fehlen noch.
- Die Testmodelle sind künstlich; als Nächstes ein echtes Projektmodell prüfen.
- Grenzwert 0.17 über Schulungsunterlagen Kanton Thurgau belegt, Norm nicht selbst nachgelesen.


## Team
Wer hat was beigetragen? (Commits zeigen es, hier kurz zusammenfassen)
| Felix | zusammen gearbeitet|
| Lilly| zusammen gearbeitet |

Beim Erstellen hat uns KI geholfen, siehe `KI_USAGE.md`.
