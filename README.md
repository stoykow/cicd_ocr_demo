# OCR mit GitHub Actions

GitHub-Repository: <https://github.com/stoykow/cicd_ocr_demo>

Dieses Mini-Projekt zeigt eine sehr einfache CI/CD-Idee:

```text
Bild in den Ordner bilder/ legen
-> Commit
-> Push
-> GitHub Actions startet
-> Tesseract OCR liest Text aus dem Bild
-> Textdateien liegen als Artefakt bereit
```

## Ordner

```text
ocr-github-action-demo/
├── bilder/
│   └── README.md
├── .github/
│   └── workflows/
│       └── ocr.yml
├── .gitignore
└── README.md
```

## Benutzung

1. Eine Bilddatei in den Ordner `bilder/` legen.
2. Unterstützte Formate: `.png`, `.jpg`, `.jpeg`, `.tif`, `.tiff`
3. Änderung committen.
4. Nach GitHub pushen.
5. In GitHub unter `Actions` den Workflow `OCR Bild zu Text` öffnen.
6. Das Artefakt `ocr-ergebnisse` herunterladen.

## Was macht die Pipeline?

Die Pipeline:

- startet bei Änderungen im Ordner `bilder/`
- installiert Tesseract OCR auf einem Ubuntu-Runner
- liest alle Bilder im Ordner `bilder/`
- erzeugt pro Bild eine `.txt`-Datei
- stellt die Textdateien als Artefakt bereit

## Sprache

Die OCR nutzt Deutsch und Englisch:

```bash
tesseract "$file" "ocr-ergebnisse/$name" -l deu+eng
```

Wenn nur Deutsch benötigt wird:

```bash
tesseract "$file" "ocr-ergebnisse/$name" -l deu
```

## Unterrichtsidee

Gute Fragen an die Teilnehmenden:

- Was ist hier der Trigger?
- Wo läuft Tesseract?
- Warum wird das Ergebnis nicht automatisch ins Repository geschrieben?
- Was ist ein Artefakt?
- Was passiert, wenn das Bild unscharf ist?
- Was passiert, wenn keine Bilddatei im Ordner liegt?

## Grenzen

Das ist keine produktive OCR-Lösung. Für den Unterricht ist es aber gut geeignet, weil der CI/CD-Ablauf sichtbar wird.
