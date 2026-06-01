# ZHAW S4 — Prüfungszusammenfassung

MkDocs + Material Projekt für die Prüfungszusammenfassung des 4. Semesters (ZHAW Applied Digital Life Science).

Fächer: **NeuNe · OrgChem · ISP · MCS · DaS · DSV**

---

## Live-Site

> Nach dem ersten Deploy unter: `https://<dein-github-username>.github.io/<repo-name>/`

---

## Setup-Vorgehen

### Voraussetzungen

- [Python 3.x](https://www.python.org/downloads/) installiert
- [Git](https://git-scm.com/) installiert
- GitHub-Account

---

### 1. Lokale Entwicklungsumgebung

**MkDocs Material installieren:**

```bash
pip install mkdocs-material
```

**Lokalen Dev-Server starten:**

```bash
cd 4.Semester
mkdocs serve
```

Die Seite ist dann unter `http://127.0.0.1:8000` erreichbar. Änderungen werden automatisch neu geladen.

---

### 2. GitHub Repository einrichten

**Neues Repository auf GitHub erstellen:**

1. Gehe zu [github.com/new](https://github.com/new)
2. Repository-Name wählen (z.B. `zhaw-s4-zusammenfassung`)
3. **Public** wählen (für GitHub Pages kostenlos)
4. Repository erstellen (ohne README, ohne .gitignore)

**Lokales Git initialisieren und pushen:**

```bash
cd 4.Semester
git init
git add .
git commit -m "Initial commit: MkDocs S4 Zusammenfassung"
git branch -M main
git remote add origin https://github.com/<dein-username>/<repo-name>.git
git push -u origin main
```

---

### 3. GitHub Pages aktivieren

Nach dem ersten Push läuft automatisch der GitHub Actions Workflow (`.github/workflows/deploy.yml`), der die Seite auf dem Branch `gh-pages` deployt.

**GitHub Pages aktivieren:**

1. Im Repository auf **Settings** gehen
2. Links auf **Pages** klicken
3. Unter **Source** → **Deploy from a branch** wählen
4. Branch: `gh-pages`, Ordner: `/ (root)` → **Save**

Nach ~1 Minute ist die Seite live unter:
```
https://<dein-username>.github.io/<repo-name>/
```

---

### 4. Inhalt aktualisieren

Markdown-Dateien im Ordner `docs/` bearbeiten, dann:

```bash
git add .
git commit -m "Update: <beschreibung>"
git push
```

Der Workflow deployt die Änderungen automatisch.

---

### 5. Manueller Deploy (ohne GitHub Actions)

Falls du direkt von lokal deployen möchtest:

```bash
mkdocs gh-deploy
```

---

## Projektstruktur

```
4.Semester/
├── docs/
│   ├── index.md        # Übersichtsseite
│   ├── neune.md        # Neural Networks
│   ├── orgchem.md      # Organische Chemie
│   ├── isp.md          # Image & Signal Processing
│   ├── mcs.md          # Modellierung komplexer Systeme
│   ├── das.md          # Data and Society
│   └── dsv.md          # Digital Storytelling & Visualisation
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Actions Deploy
├── mkdocs.yml          # MkDocs Konfiguration
└── README.md           # Diese Datei
```

---

## Nützliche Befehle

| Befehl | Beschreibung |
|--------|-------------|
| `mkdocs serve` | Lokaler Dev-Server mit Hot-Reload |
| `mkdocs build` | Statische Seite in `site/` bauen |
| `mkdocs gh-deploy` | Direkt auf GitHub Pages deployen |
| `pip install mkdocs-material --upgrade` | Material aktualisieren |
