# Using this wiki (ideas)

An LLM wiki: an agent maintains interlinked markdown pages compiled from
raw sources. You don't hand-edit the pages — you feed sources and run skills.

## Add new material
1. Drop any source file (.md / .txt / .pdf / .docx — transcripts, notes,
   docs) into `_source/_inbox/`.
2. Run the `wiki-ingest` skill ("ingest this wiki"). It extracts facts,
   writes/updates atomic pages, adds [[backlinks]], tags each fact
   ✅/⚠️/❓, appends to `log.md`, and moves the source out of `_inbox/`.
   It never fabricates.

## Check health
Run the `wiki-audit` skill ("audit this wiki"). It reports Structural /
Consistency / Trust / Coverage and lists what to fix or fill (❓ gaps).

## Structure
- `index.md` — the map; start here.
- `<page-type>/` — atomic pages (one concept each), densely [[linked]].
- `WIKI.md` — the manifest (page-types + schema).
- `log.md` — provenance (append-only).
- `_source/_inbox/` — drop zone for new material.
- Status tags: ✅ verified · ⚠️ estimate · ❓ gap.

Don't hand-edit a generated rollup; edit atomic pages, or feed sources.
