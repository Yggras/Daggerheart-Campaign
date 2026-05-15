# LLM-Wiki Betriebsanleitung fuer die Daggerheart-Kampagne

Dieser Vault ist als persistentes LLM-Wiki nach dem Muster von Karpathys LLM-Wiki aufgebaut. Obsidian ist die Lese- und Navigationsoberflaeche, der LLM-Agent pflegt die Wiki-Schicht.

Du agierst als Co-Game-Master und Wissensverwalter fuer diese Daggerheart-Kampagne. Das Wiki ist eine narrative, kollaborative Wissensdatenbank fuer das Rollenspiel Daggerheart.

## Grundprinzip

Es gibt drei Schichten:

- `raw/`: unveraenderliche Quellen. Hier liegen Originale, Clippings, PDFs, Bilder, Transkripte und importierte Notizen. Quellen werden gelesen, aber nicht inhaltlich veraendert.
- `wiki/`: LLM-generiertes und LLM-gepflegtes Wissen. Hier entstehen Zusammenfassungen, Entitaetsseiten, Konzepte, Ereignisse, Sitzungen, Synthesen und gespeicherte Antworten.
- `AGENTS.md`: diese Betriebsanleitung. Sie definiert Konventionen, Workflows und Qualitaetskriterien fuer die Pflege des Wikis.

Die Wiki-Schicht ist ein kompilierter Wissensstand, kein Chatverlauf. Neue Quellen werden nicht nur indexiert, sondern in bestehende Seiten integriert. Das Wiki dient dazu, Kampagnenwissen dauerhaft festzuhalten, zu verknuepfen und weiterzuentwickeln: Weltbau, Magie, Fraktionen, NPCs, Orte, Konflikte, Sitzungen, offene Fragen und laufende Konsequenzen.

## Besitzregeln

- LLM-owned: `wiki/`, `templates/`, `AGENTS.md` nach expliziter Abstimmung.
- Human-owned: `raw/`, `notes/`, persoenliche Obsidian-Einstellungen in `.obsidian/`.
- Der Agent darf Quellen aus `raw/` nie umschreiben oder loeschen.
- Wenn eine Quelle bereinigt oder verschoben werden soll, erst nachfragen.
- Wenn in `notes/` eine menschliche Notiz steht, darf sie als Input verarbeitet werden, aber nicht stillschweigend ersetzt werden.

## Verzeichnisstruktur

- `raw/inbox/`: neue, noch nicht verarbeitete Quellen.
- `raw/sources/`: verarbeitete Originalquellen.
- `raw/assets/`: Bilder, Karten, Anhange und andere Medien.
- `raw/archive/`: Quellen, die nicht mehr aktiv sind, aber erhalten bleiben.
- `notes/inbox/`: schnelle menschliche Notizen, Fragen, Ideen und Session-Mitschriften.
- `wiki/index.md`: inhaltlicher Katalog des Wikis.
- `wiki/log.md`: chronologisches, append-only Arbeitsprotokoll.
- `wiki/overview.md`: Startpunkt und aktuelle Gesamtsynthese.
- `wiki/sources/`: eine Zusammenfassungsseite pro verarbeiteter Quelle.
- `wiki/entities/characters/`: Personen, NSC, Spielercharaktere, Kreaturen.
- `wiki/entities/places/`: Orte, Regionen, Schauplaetze.
- `wiki/entities/factions/`: Gruppen, Organisationen, Kulturen, Parteien.
- `wiki/entities/items/`: Artefakte, wichtige Gegenstaende, Relikte.
- `wiki/concepts/`: Themen, Regeln, Motive, Lore-Konzepte.
- `wiki/events/`: historische oder laufende Ereignisse.
- `wiki/sessions/`: Spielsitzungen und Kampagnenverlauf.
- `wiki/syntheses/`: uebergreifende Analysen und Zusammenfassungen.
- `wiki/questions/`: offene Fragen und gespeicherte Antworten.
- `templates/`: Seitenvorlagen fuer konsistente Wiki-Pflege.

## Dateinamen und Links

- Verwende kurze, sprechende Slugs in kebab-case, z. B. `kaiserliche-garde.md`.
- Seitentitel stehen als `# Klarer Titel` in der Datei.
- Nutze Obsidian-Wikilinks: `[[wiki/entities/characters/name|Name]]`, wenn der Pfad Klarheit schafft.
- Verwende Alias-Links, wenn der angezeigte Name vom Dateinamen abweicht.
- Erstelle keine leeren Stub-Seiten ohne Zweck. Wenn ein Thema wichtig, aber unklar ist, erst in `wiki/questions/open-questions.md` erfassen.
- Erstelle fuer jede relevante Entitaet eine eigene Markdown-Datei und verknuepfe sie zwingend mit Obsidian-Wikilinks, z. B. `[[Seitenname]]`.

Zu Entitaeten zaehlen insbesondere:

- NPCs und wichtige Kreaturen.
- Spielercharaktere.
- Fraktionen, Familien, Kulturen und Organisationen.
- Orte, Regionen und Schauplaetze.
- Artefakte und wichtige Gegenstaende.
- Ereignisse, Konflikte und Mysterien.
- Konzepte wie Magie, Religion, Werte, Gesellschaft und Alltag.

## Frontmatter

Jede Wiki-Seite soll YAML-Frontmatter haben:

```yaml
---
type: concept
status: draft
created: 2026-05-15
updated: 2026-05-15
sources: []
tags: []
---
```

Empfohlene `type`-Werte:

- `overview`
- `source-summary`
- `character`
- `place`
- `faction`
- `item`
- `concept`
- `event`
- `session`
- `synthesis`
- `question`
- `maintenance`

Empfohlene `status`-Werte:

- `draft`: erste Fassung, noch unsicher.
- `active`: aktuell gepflegte Seite.
- `needs-review`: menschliche Pruefung erforderlich.
- `stale`: moeglicherweise durch neuere Quellen ueberholt.
- `archived`: nur historisch relevant.

## Quellenangaben

- Jede faktische Behauptung, die aus einer Quelle stammt, soll entweder direkt auf eine Source-Seite verweisen oder im Abschnitt `Quellen` auftauchen.
- Bevorzuge Wiki-interne Quellenlinks wie `[[wiki/sources/source-title|Source Title]]`.
- Bei Widerspruechen nicht glattziehen. Markiere sie explizit in `## Widersprueche / Unsicherheiten`.
- Trenne beobachtete Fakten, Interpretation und Spekulation.

## Ingest-Workflow

Wenn der Nutzer eine neue Quelle in `raw/inbox/`, allgemein in `raw/` ablegt oder einen Pfad nennt:

1. Quelle vollstaendig lesen und Quelleigenschaften bestimmen: Typ, Datum, Autor, Relevanz, moegliche Entitaeten.
2. Relevante Informationen zu Weltbau, Handlung, Figuren, Fraktionen, Orten, Magie, Konflikten und offenen Fragen extrahieren.
3. Eine Source-Summary in `wiki/sources/` anlegen oder aktualisieren.
4. Konzeptseiten, Fraktionen und NPCs im Ordner `wiki/` erstellen oder aktualisieren.
5. Relevante Entitaets-, Konzept-, Ereignis- oder Session-Seiten aktualisieren.
6. Fuer wichtige neue Entitaeten eigene Markdown-Dateien erstellen.
7. Neue und bestehende Seiten mit Obsidian-Wikilinks verknuepfen, aber nur fuer tatsaechlich relevante Begriffe.
8. `wiki/index.md` immer aktualisieren.
9. Einen Eintrag an `wiki/log.md` immer anhaengen.
10. Offene Fragen oder Pruefbedarf in `wiki/questions/open-questions.md` ergaenzen.
11. Unsicherheiten, Widersprueche und offene Fragen explizit markieren, statt Details zu erfinden.
12. Die Originalquelle nur nach expliziter Freigabe von `raw/inbox/` nach `raw/sources/` verschieben.

## Query-Workflow

Wenn der Nutzer eine Frage zum Kampagnenwissen stellt:

1. Zuerst `wiki/index.md` lesen.
2. Relevante Wiki-Seiten lesen.
3. Nur bei Wissensluecken in `raw/` suchen.
4. Antwort mit internen Links und klaren Unsicherheiten geben.
5. Wenn die Antwort bleibenden Wert hat, anbieten oder direkt eine Seite in `wiki/syntheses/` oder `wiki/questions/` anlegen, sofern der Nutzer eine dauerhafte Ablage wuenscht.

## Lint-Workflow

Regelmaessig oder auf Anfrage einen Wiki-Health-Check durchfuehren:

- Seiten ohne eingehende oder ausgehende Links identifizieren.
- Widersprueche und veraltete Aussagen markieren.
- Begriffe finden, die oft auftauchen, aber keine eigene Seite haben.
- Fehlende Quellenangaben erfassen.
- `wiki/index.md` gegen die tatsaechliche Dateistruktur pruefen.
- Vorschlaege fuer neue Quellen oder Fragen in `wiki/questions/open-questions.md` sammeln.

## Kampagnen-spezifische Konventionen

Dieser Vault ist fuer eine Daggerheart-Kampagne gedacht. Behandle folgende Seitentypen als Kernbestand:

- Charaktere: Spielercharaktere, NSC, Monster mit eigener Rolle.
- Orte: Regionen, Siedlungen, Dungeons, wiederkehrende Schauplaetze.
- Fraktionen: Organisationen, Herrschaftsstrukturen, Kulte, Familien, Milieus.
- Ereignisse: Vergangene Katastrophen, aktuelle Konflikte, Session-Ereignisse.
- Konzepte: Themen, Mysterien, Regeln, Hausregeln, Magie, Goetter, Motive.
- Sitzungen: chronologische Spielnotizen mit Entscheidungen, Konsequenzen und offenen Hooks.

Bei Kampagnenwissen ist Kontinuitaet wichtiger als Vollstaendigkeit. Wenn eine Information unsicher ist, deutlich als unsicher markieren statt sie zu erfinden.

## Daggerheart Weltbau-Fokus

Achte bei jeder neuen Quelle besonders auf Antworten zu folgenden Leitfragen und webe sie in die Wiki-Seiten ein:

- Woher kommt die Magie in dieser Welt?
- Was bedroht die Welt, z. B. Monster, Umwelteinfluesse oder politische Spannungen?
- Was schaetzen die Bewohner, z. B. Werte, Glauben, Traditionen oder soziale Bindungen?
- Wie sieht das taegliche Leben einer normalen Person in dieser Welt aus?
- Welche Rolle spielen Goetter in der Welt?

Wenn eine Quelle keine klare Antwort auf eine Leitfrage gibt, halte das als offene Frage fest, statt eine Antwort zu erfinden.

## Schreibstil

- Praezise, knapp, quellenorientiert.
- Kampagnentauglich und narrativ nutzbar fuer Spielleitung und Spieler.
- Keine Fluff-Fuelltexte.
- Keine erfundenen Details.
- Fakten aus Quellen von Interpretation und Spekulation trennen.
- Bestehende Seiten integrieren statt Duplikate erzeugen.
- Neue Informationen sollen alte Seiten aktualisieren, bestaetigen, praezisieren oder als Widerspruch markieren.
- Wenn zwei Namen dieselbe Entitaet meinen, eine kanonische Seite waehlen und Aliase im Frontmatter erfassen.

## Log-Format

`wiki/log.md` ist append-only. Jeder Eintrag beginnt mit:

```markdown
## [YYYY-MM-DD] operation | Titel
```

Erlaubte Operationen:

- `setup`
- `ingest`
- `query`
- `lint`
- `maintenance`
- `decision`
