# Checks

| Datei | Werkzeug | Inhalt |
|---|---|---|
| `Team2_U-Wert_Berechnung.ipynb` | Python 3.12, IfcOpenShell 0.9.0.post1, ifctester 0.9.0, pandas (Colab oder lokal) | **MVP v0.2:** Aussenwände finden, U aus `aufbau.csv` berechnen (DIN EN ISO 6946), ins IFC schreiben, IDS prüfen, Negativfall, Heizlast-Bezug |
| `aufbau.csv` | Text/Excel (Trennzeichen `;`) | Wandaufbau pro Wandtyp: Schicht, d, λ bzw. R, Belüftung, Quelle, Status |
| `Team2_U-Wert_Starter.ipynb` | wie oben | Starter-Notebook unseres Dozenten (unverändert) |

`aufbau.csv` bearbeiten: in Excel öffnen (Trennzeichen Semikolon), Werte prüfen, Spalte `Status` auf `geprüft` setzen, als CSV (UTF-8) speichern und hochladen. Das Notebook liest die Datei bei jedem Lauf neu.
