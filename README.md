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
Welche Objekte (Scope), welcher Datenpfad (Pset.Property, Einheit), welche Regel?

## Output
Wo liegt das Ergebnis (`results/`)? Jede Zeile: GlobalId, Objekt, Ist-Wert, Soll-Wert, Ergebnis, Grund.

## Setup
Was muss installiert sein? (Version angeben, z. B. IFC-Lite 0.41.0, Python 3.12)

## Ausführen
```
# exakter Befehl oder Klickpfad, Schritt für Schritt
```

## Testfälle
| Fall | Datei | Erwartet | Tatsächlich |
|---|---|---|---|
| positiv | | bestanden | |
| negativ | | durchgefallen | |

## Grenzen und offene Punkte
- 

## Team
Wer hat was beigetragen? (Commits zeigen es, hier kurz zusammenfassen)
