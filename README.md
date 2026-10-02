# Meine Taschenrechner-App

## Was macht das Projekt?
Dies ist eine einfache Taschenrechner-Anwendung in Python, die grundlegende mathematische Operationen wie Summe und Differenz berechnet. Sie dient als Testfall für eine CI/CD-Pipeline mit GitHub Actions.

## Pipeline im Überblick
Die Pipeline besteht aus zwei Jobs:
1. **test**: Checkt den Code aus, installiert Abhängigkeiten mit Cache-Unterstützung, führt die automatisierten Tests mit `pytest` aus, paketiert die Anwendung in eine ZIP-Datei und lädt sie als Artifact hoch.
2. **deploy**: Lädt das Artifact herunter, prüft (simuliert) Deployment-Zugangsdaten sicher und erstellt automatisch ein GitHub Release mit der ZIP-Datei.

## Trigger
Die Pipeline startet bei:
- Einem `push` auf den Branch `main`.
- Einem `pull_request` auf beliebige Branches.

## Secrets und Environment
- **Environment**: Die Pipeline nutzt das Environment `production`, um Deployment-Schritte zu schützen.
- **Secrets**: Es wird das Secret `DEPLOY_TOKEN` verwendet (wird nur als Länge ausgegeben, nicht im Klartext). Das Standard-Secret `GITHUB_TOKEN` wird für das Erstellen des Releases benötigt.

## Deployment
Beim Deployment auf dem `main`-Branch wird automatisch ein GitHub Release (z. B. `v1.0.123`) erstellt. Die paketierte Anwendung (ZIP) wird als Asset an dieses Release angehängt. Über die "Releases"-Seite auf GitHub kann das Ergebnis geprüft und heruntergeladen werden.

## Lokal ausführen
Um das Projekt lokal auszuführen und zu testen, nutze folgende Befehle:

```bash
# Virtuelle Umgebung erstellen
python -m venv .venv

# Virtuelle Umgebung aktivieren (Windows)
.venv\Scripts\activate
# (macOS/Linux: source .venv/bin/activate)

# Abhängigkeiten installieren
python -m pip install -r requirements.txt

# Tests ausführen
python -m pytest -v

# Build (optional)
mkdir -p build
python -m zipfile -c build/app-paket.zip src/
```