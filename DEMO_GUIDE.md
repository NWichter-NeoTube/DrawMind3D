# DrawMind3D — Demo Video Leitfaden

Ziel: 2-4 Minuten Video, das den kompletten Workflow zeigt.

## Empfohlener Aufbau (3 min)

### 1. Intro (15 sek)
- Titel-Slide: "DrawMind3D — PDF-Annotationen zu 3D-Features"
- Kurz das Problem erklaren: Technische Zeichnung + 3D-Modell, manuelle Zuordnung ist zeitaufwendig

### 2. Web UI Demo (90 sek)
**Vorbereitung:** Web-Server starten (`uv run python web/app.py`), NIST FTC-09 PDF + STEP bereithalten

- Browser offnen: `http://localhost:8000`
- PDF + STEP hochladen (FTC-09 empfohlen — zeigt LLM-Mehrwert am besten)
- "Enable LLM Enhancement" aktivieren
- Analyse starten, kurz auf Ergebnis warten
- Ergebnis zeigen:
  - **Summary-Statistiken**: Anzahl Annotations, Holes, Matches, Avg Confidence
  - **3D-Viewer**: Modell drehen, Hole-Features sichtbar
  - **PDF-Viewer**: Annotationen mit Bounding Boxes
  - **Matches-Tabelle**: Auf einen Match klicken → 3D-Feature wird hervorgehoben

### 3. CLI / Output (30 sek)
- Terminal zeigen: `uv run python run.py --pdf nist_ftc_09.pdf --step nist_ftc_09.stp -v`
- JSON-Output kurz zeigen: Match mit `annotation_text`, `feature_3d_ref`, `confidence`

### 4. Evaluation (30 sek)
- Ergebnis-Chart zeigen (aus `data/evaluation/presentation/`)
- Zahlen nennen: "F1 82%, Recall 94%, Linking 90%, getestet auf 7 Testfallen"
- Vergleich zeigen: Ohne LLM vs. mit LLM (FTC-09: 12% → 88% F1)

### 5. Architektur (15 sek)
- Pipeline-Diagramm aus README kurz einblenden
- Kernpunkte: PyMuPDF → Regex → Vision LLM → OCP → Hungarian Matching → JSON

## Tipps

- **Bester Demo-Fall:** FTC-09 (NIST) — zeigt den LLM-Mehrwert dramatisch
- **Zweitbester:** SYN-05 (100% F1) — zeigt perfektes Ergebnis bei synthetischen Daten
- **Reihenfolge:** Immer zuerst das Ergebnis zeigen, dann erklaren wie es funktioniert
- **Geschwindigkeit:** LLM-Analyse dauert ~30-60 Sek, ggf. vorher laufen lassen und vorspulen
- **Fallback zeigen:** Kurz `--no-llm` erwahnen — Pipeline funktioniert auch ohne API-Key

## Zu vermeiden

- Nicht zu lange auf Code eingehen — Fokus auf Ergebnisse und UI
- Nicht alle 7 Testfalle durchgehen — 1-2 reichen
- Docker-Setup nicht live zeigen — zu langsam, lieber erwahnen

## Dateien fur Slides

- `data/evaluation/presentation/01_f1_comparison.svg` — F1 Vergleich mit/ohne LLM
- `data/evaluation/presentation/02_metrics_overview.svg` — Alle Metriken
- `data/evaluation/presentation/03_llm_impact.svg` — LLM Impact horizontal
- `data/evaluation/presentation/04_summary_table.svg` — Ergebnis-Tabelle
