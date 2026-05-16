---
type: maintenance
status: active
created: 2026-05-15
updated: 2026-05-16
sources: []
tags: [log]
---

# Log

Chronologisches, append-only Protokoll der Wiki-Arbeit.

## [2026-05-15] setup | LLM-Wiki initialisiert

- Karpathys LLM-Wiki-Muster als lokale Obsidian-Architektur umgesetzt.
- Schichten angelegt: `raw/`, `wiki/`, `notes/`, `templates/`.
- `AGENTS.md` als Betriebsanleitung fuer kuenftige Agent-Sessions erstellt.
- Startseiten, Index, Log und Open-Questions-Seite angelegt.

## [2026-05-15] ingest | Startbestand aus raw/inbox

Pages written: 00-kanon-und-adaptionspolitik, 01-kampagnenueberblick, 02-praemisse-und-ton, 03-weyard-und-kosmologie, 04-elemente-und-psynergy, 05-dschinn-regelrahmen, 06-fraktionen, 07-orte-und-regionen, 08-nsc-und-schluesselfiguren, 09-session-zero, 10-erster-handlungsbogen, 11-offene-fragen-und-entscheidungen, 12-glossar, kampagnenkern, psynergy, alchemie, venus, mars, jupiter, merkur, dschinn, leuchttuerme, elementsterne, hope-und-fear, utility-psynergy, beschwoerungen, psynergy-stein, psynergy-vortex, weltverfall, leuchtturmkrise, der-dschinn-in-der-mine, session-zero, weyard, weltrand, gaia-falls, altin-xian-kalay-route, vale-und-aleph-massiv, sol-sanctum, imil-und-merkur-leuchtturm, kolima, kalay-und-tolbi, gondowan-und-lalivero, prox, lemuria, hueter-des-siegels, proxeanische-rettungsfraktion, merkur-heilerorden, venus-haine-und-erdsprecher, jupiter-zirkel, haendlerliga-von-kalay-und-tolbi, dschinn-sucher, lokale-autoritaeten, tau, kiesel, esse, boee, raska, selen, dorvan, ilyen, isaac, felix, saturos, menardi, mia, ivan, garet

Pages updated: wiki/index, wiki/overview, wiki/questions/open-questions, wiki/log

## [2026-05-16] maintenance | Verarbeitete Quellen archiviert

- 13 bereits ingestierte Quellen von `raw/inbox/` nach `raw/sources/` verschoben.
- Source-Summaries in `wiki/sources/` auf die finalen Originalpfade `raw/sources/...` aktualisiert.
- `wiki-ingest` wurde zuvor so angepasst, dass kuenftige Ingests diese Verschiebung automatisch nach erfolgreichem Wiki-Update durchfuehren.
