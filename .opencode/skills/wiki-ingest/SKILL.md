---
name: wiki-ingest
description: Use when adding a new source to a wiki — a paper, article, URL, file, transcript, or any document. One ingest may touch 10-15 wiki pages.
---

# Wiki Ingest

Add a source to the wiki. Read it, discuss with the user, write a summary page, update entity/concept pages, maintain the index, overview, and log, then move the processed original source from `raw/inbox/` to `raw/sources/`.

## Pre-condition

Search for `AGENTS.md` starting from the current directory and upward, or in common wiki locations (`~/wikis/`). If not found, tell the user to run `wiki-init` first.

Read `AGENTS.md` to learn: wiki root path, source ownership rules, page frontmatter format, cross-reference convention, log entry format, index category taxonomy, and any vault-specific directory layout. Vault instructions override this skill whenever they are more specific.

## Process

### 1. Accept the source

The source can be:
- **File path inside `raw/inbox/`** — read it directly and reserve the final processed path `raw/sources/<filename>`.
- **File path inside `raw/sources/`** — read it directly; it is already processed storage, so do not move it later.
- **File path outside `raw/`** — read it directly; if a durable raw copy is needed, copy it to `raw/inbox/<filename>` before ingest, then treat that copy as the source.
- **URL** — fetch it with the available web fetch tool; save the raw capture to `raw/inbox/<slug>.<ext>` before ingest.
- **Pasted text** — save it to `raw/inbox/<slug>.md` before ingest, unless the user explicitly says not to persist it.

Never delete original sources. Never edit the contents of files under `raw/`. If the target `raw/sources/<filename>` already exists and is not the same source, stop and ask the user for a filename decision.

Before writing wiki pages, determine the final source path that will be true after ingest completes. For a source in `raw/inbox/`, this is normally `raw/sources/<filename>`. Use that final path in source-summary metadata and citations so the wiki does not need path rewrites after the move.

### 2. Read the source in full

Read all content. For long sources, read in sections. Do not skip.

### 3. Surface takeaways — BEFORE writing anything

Tell the user:
- 3-5 bullet points of key takeaways
- What entities/concepts this introduces or updates
- Whether it contradicts anything already in the wiki (read `wiki/index.md` and relevant pages to check)

Ask: **"Anything specific you want me to emphasize or de-emphasize?"**

Wait for the user's response before proceeding.

### 4. Generate the slug

Lowercase, hyphens, no special characters.
Example: "Attention Is All You Need" → `attention-is-all-you-need`

### 5. Write the source summary page

Write `wiki/sources/<slug>.md` unless `AGENTS.md` specifies a different source-summary location:

```markdown
---
type: source-summary
status: active
created: <today>
updated: <today>
source_path: raw/sources/<filename>
source_type: <paper | article | transcript | code | note | other>
source_date: <source date or unknown>
sources: [<slug>]
tags: [source, <relevant tags>]
---

# <Source Title>

**Quelle:** `raw/sources/<filename>`
**Datum ingestiert:** <today>
**Typ:** <paper | article | transcript | code | note | other>

## Summary

<2-3 paragraph synthesis — your own words, not abstract copy-paste>

## Key Takeaways

- <bullet>

## Entities & Concepts

<list of entities/concepts as [[slug]] links>

## Relation to Other Wiki Pages

<how this connects to or updates existing knowledge>
```

### 5b. Cite as you write — do not skip

While drafting the Summary, Key Takeaways, and any other prose section, every
non-common-knowledge factual claim must carry a footnote. Read the **Citations**
section in `AGENTS.md` for the full convention.

Two citation kinds, three valid targets:

```
Quote:     [^N]: <target> <locator> — "<verbatim quote>"
Synthesis: [^N]: <target> <locator> [synthesis] — <what supports the claim>

<target> is one of:
  [[wiki/sources/source-slug|Source Title]] — a source wiki page (preferred for the source you're ingesting)
  raw/sources/<file>   — final processed source path, for drive-by citations to local files
  <URL>                — a live URL or post
```

For the source being ingested, use `[[wiki/sources/<this-source-slug>|<Source Title>]]` and cite the final processed raw path in the locator, for example `raw/sources/<filename>:12-18`. The source page is created during ingest, and the raw file is moved there only after all wiki updates succeed.

If you cannot produce either citation kind for a claim, you do not have a
citation. Find one, weaken the claim ("the paper suggests..."), or drop it.

Footnotes go at the bottom of the page, below all sections. Number them
sequentially in order of first reference.

### 5c. Self-check before continuing

Re-read the draft once. Scan for unfootnoted factual claims — this is the most
common failure mode in long ingest sessions. For each, add a footnote or revise
the wording. Only then move on to entity pages.

### 6. Update entity and concept pages

For each entity/concept touched by this source:

- **Page exists:** Read it, add to or update the relevant section, add this source to frontmatter `sources` list, update `updated` date
- **Page doesn't exist:** Create it in the directory required by `AGENTS.md`, for example `wiki/entities/characters/`, `wiki/entities/places/`, `wiki/entities/factions/`, `wiki/entities/items/`, `wiki/concepts/`, `wiki/events/`, or `wiki/sessions/`:

```markdown
---
type: <character | place | faction | item | concept | event | session | synthesis | question>
status: draft
created: <today>
updated: <today>
aliases: []
sources: [<this-source-slug>]
tags: [<entity | concept | relevant tags>]
---

# <Name>

## Beschreibung

<synthesis across all sources that discuss this>

## Bekannte Fakten

<facts with source links>

## Beziehungen

<relevant wiki links>

## Widersprueche / Unsicherheiten

<known gaps or contradictions>

## Quellen

- [[wiki/sources/source-slug|Source Title]] — <one-line note>
```

### 7. Backlink audit — do not skip

Scan ALL existing pages under `wiki/` for any that mention this source's entities/concepts but don't yet link to the relevant page. Add Obsidian wikilinks with vault-appropriate paths, for example `[[wiki/entities/characters/name|Name]]`, where appropriate.

This is the step most commonly skipped. A compounding wiki's value comes from bidirectional links.

### 8. Update `wiki/index.md`

Add an entry under the correct category:
```
- [[<slug>]] — <one-line summary> _(ingested <date>)_
```

For any new entity/concept pages created, add those too.

### 9. Update `wiki/overview.md`

Re-read the current overview. If this source:
- Introduces a significant concept: add it to "Key Entities / Concepts"
- Shifts the overall understanding: update "Current Understanding"
- Raises a new question: add it to "Open Questions"

Update the frontmatter `updated` date.

### 10. Move the processed source

After the source summary, entity/concept updates, backlink audit, index update, and overview update have completed successfully, move the processed original source from `raw/inbox/<filename>` to `raw/sources/<filename>`.

Rules:
- Move only the original raw file, never delete it.
- Do not rewrite or normalize the raw file contents.
- Do not move files from `notes/`; notes are human-owned input and should remain where they are unless the user explicitly requests otherwise.
- Do not move assets or attachments unless the user explicitly requests it.
- If moving fails, leave the wiki updates in place, append the log with `Source move failed: <reason>`, report the failure, and keep the source in `raw/inbox/`.

If the source was already in `raw/sources/`, do not move it.

### 10b. Append to `wiki/log.md`

```
## [<today>] ingest | <source title>
Pages written: <slug>
Pages updated: <comma-separated list>
Source moved: raw/inbox/<filename> -> raw/sources/<filename>
```

If the source was already in `raw/sources/`, write `Source retained: raw/sources/<filename>` instead. If the move failed, write `Source move failed: <reason>` instead.

## Common Mistakes

- **Appending chronological updates instead of editing in-place** — Wiki pages are living documents, not journals. Do not add sections like `## April 27 update:` or `**Update:**` followed by new content. Update the relevant section in-place, bump the `updated` frontmatter date, and record what changed in `log.md`. The log is the append-only record; pages are the current truth.
- **Skipping the backlink audit (step 7)** — A wiki's value compounds through bidirectional links. Always scan existing pages for entities this source introduces.
- **Summarizing the abstract instead of synthesizing** — The Summary section should reflect your own synthesis, not a rephrased abstract.

### 11. Report to user

- Summary page: `wiki/sources/<slug>.md`
- Entity/concept pages created or updated: <list>
- Pages that received backlinks: <list>
- Index and overview updated
- Source moved: `raw/inbox/<filename>` -> `raw/sources/<filename>` or source retained in `raw/sources/`
