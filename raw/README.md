---
type: maintenance
status: active
created: 2026-05-15
updated: 2026-05-15
sources: []
tags: [raw, sources]
---

# Raw Sources

`raw/` ist die unveraenderliche Quellenschicht des Wikis. Der LLM-Agent darf diese Dateien lesen, aber nicht inhaltlich veraendern.

## Ordner

- `inbox/`: neue Quellen, die noch nicht verarbeitet wurden.
- `sources/`: bereits verarbeitete Originalquellen.
- `assets/`: Bilder, Karten, PDFs, Audiodateien und andere Medien.
- `archive/`: alte oder nicht mehr aktive Quellen, die erhalten bleiben sollen.

## Empfehlung

Lege pro Quelle moeglichst eine eigene Datei an. Gute Dateinamen enthalten Datum und Kurzbeschreibung, z. B. `2026-05-15-session-01-notes.md`.
