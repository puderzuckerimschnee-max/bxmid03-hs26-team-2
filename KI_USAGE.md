# KI-Einsatz

| Datum | Werkzeug | Zweck | Was wurde übernommen | Wie geprüft |
|---|---|---|---|---|
| 01.11.2026 | Claude (Anthropic) | Testmodelle erstellen | `models/Team2_Wand_U_ok.ifc` (aus dem Kursmodell `Demo_Holzrahmen_korrigiert.ifc`, U-Wert ergänzt) | in IFC-Lite 5.3.1 geöffnet, Wand und Eigenschaften sichtbar |
| 02.11.2026 | Claude (Anthropic) | YAML-Vorlage auf unseren U-Wert anpassen | `requirements/Team2_U-Wert.yaml` | mit unserer Anforderung und dem Prozess vom 19.10. verglichen |
| 02.11.2026 | Claude (Anthropic) | IDS-Datei zur YAML erstellen (idslight.com lud am 12.10. nicht) | `requirements/Team2_U-Wert.ids` | in IFC-Lite 5.3.1 geladen: «Document is valid»; positiv 1 passed, negativ 1 failed |


Selbst gemacht: Prozessmodell IST/SOLL (Abgabe 19.10.), Prüfung in IFC-Lite
und Vergleich mit dem erwarteten Ergebnis. Grenzwerte selber ausgedacht und als Anforderung angegeben. Negativer Testfall erstellt in IFC-Lite 5.3.1: «must exist», 1 failed.
