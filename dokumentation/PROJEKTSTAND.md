# Projektstand Team 2 · U-Wert der Gebäudehülle

BFH Minor BXMid03 «Data Management und BIM», HS 2026/27
Stand: **03.11.2026** · 

Diese Datei beantwortet drei Fragen: **Wo stehen wir? Was liegt wo? Was ist noch offen?**

---

## 1. Worum es geht (in 3 Sätzen)

Die Bauphysik braucht für den Energienachweis die U-Werte der Aussenwände. Heute fehlen sie im IFC-Modell, darum wird per Telefon nachgefragt und in Excel gerechnet.
Unser MVP berechnet den U-Wert aus dem Wandaufbau, schreibt ihn ins Modell und prüft ihn automatisch mit einer IDS-Regel.

**Soll-Prozess:** Bauphysik liefert Aufbau → U-Wert → Modell → IDS-Prüfung

---

## 2. Wo stehen wir? (Zeitachse)

| Datum | Meilenstein | Was wir abgegeben bzw. gemacht haben | Status |
|---|---|---|---|
| 12.10.2026 | AIA-BEP-Matrix | Matrix und IDS «Wandmengen» (andere Fragestellung, Kostenplanung) | abgegeben |
| 19.10.2026 | Prozessmodell | IST/SOLL-Prozess U-Wert (`workflow/Team_2_U-Wert_Prozess_Ist_Soll.drawio.pdf`) | abgegeben |
| 27.10.2026 | Kurs Automatisierung I | Auftrag MVP v0.1, Team-Repository | erledigt |
| 02.11.2026 | **MVP v0.1** | Prüfung «U-Wert vorhanden» mit IFC-Lite an einer Testwand, positiv und negativ | in unserer Kopie; Abgabe auf Moodle: _bitte bestätigen_ |
| 03.11.2026 | Feedback Dozent | Starter-Notebook und echtes Modell `BIMcollab_Example_ARC.ifc` per Pull Request in unsere Kopie, Vorschlag zur Vertiefung | übernommen |
| 03.11.2026 | **MVP v0.2** | U-Wert aus Aufbau berechnen, ins Modell schreiben, IDS ≤ 0.28, Negativfall, Heizlast-Bezug | **in Arbeit: Werte prüfen** |
| _offen_ | Peer-Audit / nächste Abgabe | _Datum eintragen_ | _offen_ |

---

## 3. Was liegt wo?

```
README.md                    Hauptbeschreibung MVP (Problem, Input, Verarbeitung, Output, Ausführen, Testfälle)
PROJEKTSTAND.md              diese Datei: Stand, Ablage, offene Punkte
KI_USAGE.md                  wo und wie wir KI eingesetzt haben

checks/
  Team2_U-Wert_Berechnung.ipynb   MVP v0.2: unser Notebook (in Colab ausführen)
  aufbau.csv                      Wandaufbau pro Wandtyp: d, λ, Quelle, Status  ← HIER arbeiten wir
  Team2_U-Wert_Starter.ipynb      Vorlage unseres Dozenten (nicht verändern)

models/
  BIMcollab_Example_ARC.ifc       echtes Architekturmodell, 70 Aussenwände, ohne U-Werte (v0.2)
  Team2_Wand_U_ok.ifc             Testwand mit U = 0.15 (v0.1, positiv)
  Team2_Wand_ohne_U.ifc           Testwand ohne U (v0.1, negativ)

requirements/
  anforderung.md                  Anforderung, Normen und Quellen
  Team2_U-Wert_Aussenwand.ids     Regel v0.2: Aussenwand, U ≤ 0.28 (vom Notebook erzeugt)
  Team2_U-Wert.ids / .yaml        Regel v0.1: U vorhanden (YAML nach Vorlage Dozent)

results/
  u_wert_aussenwaende.csv         Ergebnis v0.2 pro Wand
  u_wert_aussenwaende_negativfall.csv
  ergebnis.csv                    Ergebnis v0.1
  README.md                       Übersicht aller Läufe

workflow/
  prozess.md                      wo das MVP im Soll-Prozess steht
  Team_2_U-Wert_Prozess_Ist_Soll.drawio(.pdf)   Abgabe 19.10.

poster/                           noch leer (Vorlage Dozent)
```

**Wo liegt was online?**

| Was | Adresse |
|---|---|
| Team-Repository (offiziell, Abgabe-Link) | https://github.com/LTplus-AG/bxmid03-hs26-team-2 |
| unsere Kopie (hier arbeiten wir, weil wir im Team-Repo keine Schreibrechte haben) | https://github.com/puderzuckerimschnee-max/bxmid03-hs26-team-2 |
| Kursmaterial | https://github.com/LTplus-AG/bxmid03-hs26 |
| IFC-Lite (Prüfung im Browser) | https://www.ifclite.com |

---

## 4. Wie arbeiten wir? (Kurzanleitung)

**Notebook laufen lassen**
1. In unserer Kopie `checks/Team2_U-Wert_Berechnung.ipynb` öffnen
2. «In Colab öffnen» → «Laufzeit» → «Alle ausführen»
3. Ergebnis steht unten in Abschnitt 11

**Wandaufbau ändern**
1. `checks/aufbau.csv` herunterladen und in Excel öffnen (Trennzeichen Semikolon)
2. Werte prüfen oder ändern, jede Zahl mit Quelle, Spalte `Status` auf `geprüft`
3. Als CSV (UTF-8) speichern, im Ordner `checks` hochladen, Notebook neu laufen lassen

**Dateien hochladen**
- Immer zuerst in den richtigen Ordner klicken, dann «Add file → Upload files», dann «Commit changes»
- Nie mehrere Ordner auf einmal hineinziehen (der Browser löst die Ordner auf)
- Zum Schluss Pull Request an das Team-Repo: «Contribute → Open pull request»

**Regel: Daten ändern, Regel beibehalten.** Fällt eine Wand durch, wird der Aufbau oder das Modell korrigiert, nicht der Grenzwert.

---

## 5. Aktuelles Ergebnis (MVP v0.2, Lauf 03.11.2026)

| Fall | IDS-Ergebnis |
|---|---|
| Modell ohne U-Werte | 0 von 70 bestanden |
| positiv: U aus `aufbau.csv` | 8 von 70 bestanden (Timberframe, U = 0.169) |
| negativ: Timberframe mit 40 mm statt 140 mm Mineralwolle | 0 von 70 bestanden (U = 0.319) |

Grenzwert: U ≤ 0.28 W/(m²K), GEG Anlage 1 Zeile 1.1. Berechnung nach DIN EN ISO 6946, λ nach DIN 4108-4:2020-11.
Heizlast-Bezug (DIN EN 12831, wie in unserer Projektarbeit 2025): Φ_T der Aussenwände ca. 18.9 kW.

**Achtung:** Diese Zahlen beruhen auf dem **Vorschlag** in `aufbau.csv`. Ändern wir den Aufbau, ändert sich das Ergebnis.

---

## 6. Entscheidungen, die wir getroffen haben

| Datum | Entscheidung | Warum |
|---|---|---|
| 01.11. | Prüfung mit IFC-Lite statt eigenem Python-Skript (v0.1) | passt zu unserem Wissensstand, im Kurs gezeigt |
| 02.11. | Regel v0.1 nach YAML-Vorlage des Dozenten, nur «U vorhanden» | die Vorlage kennt kein Wort für Grenzwerte |
| 02.11. | Negativfall v0.1 = Wand ohne U-Wert | genau unsere Schwachstelle im IST-Prozess |
| 03.11. | v0.2 mit dem Notebook des Dozenten weiterführen | U-Wert kann automatisch ins Modell geschrieben werden |
| 03.11. | Normbasis Deutschland (DIN, GEG) | passt zu unserer Heizlast-Projektarbeit nach DIN EN 12831 |
| 03.11. | Aufbau als Vorschlag von KI, wir prüfen | Modell hat keine Schichtdicken und keine λ-Werte |

---

## 7. Offene Punkte (To-do)

| # | Aufgabe | Wer | Bis | Erledigt |
|---|---|---|---|---|
| 1 | `aufbau.csv` prüfen: Quellen öffnen, Werte kontrollieren, `Status` auf `geprüft` | _Name_ | _Datum_ | ☐ |
| 2 | Klären: Welcher Dämmstoff ist «Insulation - plastic hard» (EPS, XPS, PIR)? | _Name_ | | ☐ |
| 3 | λ für Stahlbeton und Sperrholz in DIN EN ISO 10456 nachschlagen | _Name_ | | ☐ |
| 4 | Grenzwert 0.28 selbst in GEG Anlage 1 nachlesen; Anlage 1 oder Anlage 7? | _Name_ | | ☐ |
| 5 | Luftschicht Kavitätsmauerwerk: ruhend oder belüftet? | _Name_ | | ☐ |
| 6 | Eine Wand selbst von Hand nachrechnen (z.B. Cavity wall) und im README ergänzen | _Name_ | | ☐ |
| 7 | 37 verdächtige Aussenwände: Befund für den Architekten formulieren (`IsExternal`) | _Name_ | | ☐ |
| 8 | `KI_USAGE.md` korrigieren («Grenzwerte selber ausgedacht» stimmt nicht mehr) und ergänzen | _Name_ | | ☐ |
| 9 | Notebook selbst einmal in Colab laufen lassen und Ergebnis vergleichen | _Name_ | | ☐ |
| 10 | Dateien v0.2 in unsere Kopie hochladen und Pull Request an das Team-Repo | _Name_ | | ☐ |
| 11 | Ausblick: Dach, Boden, Fenster; BCF-Befund automatisch erzeugen | | | ☐ |

---

## 8. Begriffe kurz erklärt

| Begriff | Bedeutung |
|---|---|
| **IFC** | offenes Dateiformat für BIM-Modelle |
| **IDS** | Datei mit Prüfregeln für IFC-Modelle («Information Delivery Specification») |
| **Pset / Property** | Eigenschaftensatz bzw. Eigenschaft eines Bauteils, z.B. `Pset_WallCommon.ThermalTransmittance` = U-Wert |
| **GlobalId** | eindeutige Kennung eines Bauteils, damit man es im Viewer wiederfindet |
| **U-Wert** | Wärmedurchgangskoeffizient in W/(m²K), je kleiner desto besser gedämmt |
| **λ (Lambda)** | Wärmeleitfähigkeit eines Baustoffs in W/(m·K) |
| **Rsi / Rse** | Wärmeübergangswiderstand innen / aussen |
| **Fork / Kopie** | unsere eigene Kopie des Team-Repos auf GitHub |
| **Commit** | gespeicherte Änderung auf GitHub |
| **Pull Request** | Vorschlag, unsere Änderungen ins Team-Repo zu übernehmen |
| **Colab** | Google-Dienst, um Notebooks im Browser auszuführen |

---

## 9. Wie läuft unser Modell bisher?

1. Modell lesen        →  Welche Wände sind Aussenwände? Wie dick? Welche Materialien?
2. Aufbau zuordnen     →  aufbau.csv: Dicke und λ pro Schicht
3. U-Wert rechnen      →  U = 1 / (Rsi + Σ d/λ + Rse)
4. Mit Grenzwert vergleichen  →  U ≤ 0.28?
5. Ins Modell schreiben und mit IDS prüfen

# Schritt 1: Was das Modell liefert
| Was | Wo im IFC | Beispiel |
|---|---|---|
|Ist es eine Aussenwand?|Pset_WallCommon.IsExternal|TRUE bei 70 von 171 Wänden|
|Wanddicke|BaseQuantities.Width (in mm, ×0.001 → m)|340 mm|
|Materialien|Materialliste der Wand|Stone - limestone, Insulation - plastic hard, Air, Stone - brick|
|Wandfläche|BaseQuantities.NetSideArea|in m²|


---

## 10. Änderungsprotokoll dieser Datei

| Datum | Wer | Was |
|---|---|---|
| 03.11.2026 | _Name_ | Datei angelegt |
