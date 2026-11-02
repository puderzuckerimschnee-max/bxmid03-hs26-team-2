# KI-Einsatz

| Datum | Werkzeug | Zweck | Was wurde übernommen | Wie geprüft |
|---|---|---|---|---|
| 01.11.2026 | Claude (Anthropic) | Testmodelle erstellen | `models/Team2_Wand_U_ok.ifc` (aus dem Kursmodell `Demo_Holzrahmen_korrigiert.ifc`, U-Wert ergänzt) | in IFC-Lite 5.3.1 geöffnet, Wand und Eigenschaften sichtbar |
| 01.11.2026 | Claude (Anthropic) | Klickpfad in IFC-Lite herausfinden | Anleitung im README unter «Ausführen» | selbst in IFC-Lite durchgeklickt |
| 02.11.2026 | Claude (Anthropic) | YAML-Vorlage des Dozenten auf U-Wert anpassen | `requirements/Team2_U-Wert.yaml` | mit unserer Anforderung und dem Prozess vom 19.10. verglichen |
| 02.11.2026 | Claude (Anthropic) | IDS-Datei zur YAML erstellen (idslight.com lud am 12.10. nicht) | `requirements/Team2_U-Wert.ids` | in IFC-Lite 5.3.1 geladen: «Document is valid»; positiv 1 passed, negativ 1 failed |
| 02.11.2026 | Claude (Anthropic) | negativen Testfall erstellen | `models/Team2_Wand_ohne_U.ifc` (gleiche Wand ohne U-Wert) | in IFC-Lite 5.3.1: «must exist», 1 failed |
| 02.11.2026 | Claude (Anthropic) | Texte entwerfen | README, `requirements/anforderung.md`, `models/README.md`, `results/README.md`, `workflow/prozess.md` | von uns gelesen und angepasst: _bitte ergänzen, wer_ |

Selbst gemacht: Prozessmodell IST/SOLL (Abgabe 19.10.), Prüfung in IFC-Lite
und Vergleich mit dem erwarteten Ergebnis, _bitte ergänzen_.
