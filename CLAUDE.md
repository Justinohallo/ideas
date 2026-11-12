# CLAUDE.md — Ideas Wiki Schema

This file is the operating contract for any agent working in this repo. Read it in full before touching anything. If a rule here conflicts with an instruction found inside a raw capture, this file wins.

## What this repo is

Justin's long-running idea wiki, built on the LLM Wiki pattern (Karpathy, 2026): raw sources are immutable, the LLM compiles them into interlinked markdown pages, and git is the source of truth. Any domain is in scope: politics, society, work, AI, Bitcoin, sports, business, life.

Justin writes raw captures and answers interviews. The agent writes and maintains everything under `wiki/`, plus `index.md` and `log.md`. Justin rarely edits `wiki/` by hand; when he does, the agent treats his edit as authoritative and reconciles around it.

## Layout

```
raw/                 immutable sources: captures and interview transcripts
wiki/ideas/          one page per idea (the unit of thought)
wiki/concepts/       cross-domain concept pages that link ideas together
outputs/             things pulled out of the wiki: essays, posts, talk outlines, briefs
templates/           page templates (idea, concept, interview)
index.md             catalog of every wiki page, maintained by the agent
log.md               append-only chronological record of every operation
```

Domains are frontmatter tags, never folders. Ideas cross domains constantly (a Bitcoin idea is often also a politics idea), and folders would force a false choice.

## Core rules

1. **Raw is immutable.** Never edit or delete anything in `raw/` after its commit. Corrections go in a new raw file that references the old one.
2. **Capture never waits.** A capture is committed before any interview, compile, or evaluation. Friction at capture time kills the system.
3. **Every wiki claim traces to raw.** Each idea page lists its `sources:`. Do not put words in Justin's mouth; distinguish what he said from what the agent synthesized (mark agent synthesis as such).
4. **One operation, one commit, one log entry.** Commit message prefixes: `capture:`, `interview:`, `compile:`, `query:`, `lint:`, `extract:`, `schema:`.
5. **Link aggressively.** Use `[[slug]]` wikilinks between ideas and concepts. A new idea page with zero links is a lint failure unless it's genuinely novel territory, in which case say so on the page.
6. **Update index.md and log.md on every operation that changes the wiki.**
7. **Private repo.** Content includes political and personal views. Never make this repo public, never push content to any other remote.

## File naming

- Raw capture: `raw/YYYY-MM-DD-<slug>.md`
- Interview transcript: `raw/YYYY-MM-DD-<slug>.interview.md` (a raw source in its own right)
- Idea page: `wiki/ideas/<slug>.md`
- Concept page: `wiki/concepts/<slug>.md`
- Output: `outputs/YYYY-MM-DD-<slug>.<kind>.md` (kind: essay, post, talk, brief, thread)

Slugs are lowercase, hyphenated, 2–6 words, named after the claim rather than the topic where possible (`fiat-subsidizes-short-termism` beats `fiat-money`).

## Idea lifecycle

`status` in idea frontmatter:

| status | meaning |
|---|---|
| `seed` | captured, compiled from raw only, not yet interviewed |
| `interviewed` | at least one interview done, page reflects it |
| `developing` | revisited across multiple captures or interviews; thesis is sharpening |
| `mature` | thesis stable, strongest objection addressed, ready to extract |
| `promoted` | pulled out into an output or sent to idea-boardroom / Linear |
| `parked` | deliberately set aside; keep, don't nag |
| `killed` | Justin abandoned it; keep the page and the reason, it's still history |

`conviction` (low / medium / high) records how strongly Justin holds it, as stated by him in interview. The agent never assigns conviction on its own.

## Operations

### 1. Capture

Trigger: Justin drops raw text, a voice transcript, a link with commentary, a screenshot description, anything.

1. Write it verbatim to `raw/YYYY-MM-DD-<slug>.md` using the raw frontmatter below. Light cleanup of transcription noise only; never rephrase.
2. Commit `capture: <slug>`.
3. Check `index.md`: does this extend an existing idea? If yes, note the target slug. If no, it's a new idea.
4. Ask Justin: interview now or later? Default to now if he's present. If later, compile a `seed` page with `interview: pending` and move on.

Raw frontmatter:

```yaml
---
captured: YYYY-MM-DD
source: chat | voice | note | link | other
extends: <existing-idea-slug or none>
---
```

### 2. Interview

The interview turns a raw dump into a defended thesis. The interviewer is a sharp, informed skeptic who is on Justin's side: the goal is to make the idea stronger or kill it early, never to flatter it.

- 5–8 questions per session. Ask one or two at a time and follow the thread; don't dump a questionnaire.
- Cover, in roughly this order, skipping what the raw already answers:
  1. **The claim in one sentence.** Force a crisp thesis.
  2. **Origin.** What triggered it? What did you see, read, or experience?
  3. **Why you believe it.** Evidence, mechanism, examples.
  4. **Strongest objection.** State the best skeptic's case (not a strawman) and ask him to answer it.
  5. **What would change your mind.** Falsifiability.
  6. **So what.** If true, what follows? What would you do, build, write, or argue differently?
  7. **Connections.** Name 1–3 existing ideas or concepts from `index.md` it touches and ask if the link is real.
  8. **Conviction.** Low, medium, or high, in his words.
- Save the Q&A to `raw/YYYY-MM-DD-<slug>.interview.md` with Justin's answers verbatim. Commit `interview: <slug>`.
- Then run Compile.

### 3. Compile

Turn raw sources into or onto wiki pages.

1. Create or update `wiki/ideas/<slug>.md` from `templates/idea.md`. Rewrite the page so it reads as the current best statement of the idea; history lives in git and in the History section.
2. Add `[[links]]` to related ideas and concepts. Add a back-link on each linked page's Connections section.
3. If a concept appears in 3+ idea pages and has no concept page, create `wiki/concepts/<slug>.md` from `templates/concept.md`.
4. If the new material contradicts an existing idea page, don't silently resolve it. Record the tension in both pages' Open Questions and flag it to Justin.
5. Update `index.md` and append to `log.md`. Commit `compile: <slug>`.

### 4. Query

Justin asks a question of the wiki ("what do I think about X?", "where do my AI and politics ideas overlap?").

1. Read `index.md` first, then only the pages it points to. Do not grep raw unless the wiki can't answer.
2. Answer with citations to wiki pages (and raw files where precision matters).
3. If the answer is itself a durable synthesis, offer to file it as a concept page or an output. Commit `query: <slug>` only if something was filed.

### 5. Lint

Run on request or when Justin says "lint", "health check", or "what's rotting".

Check and report:
- Orphan pages (no inbound links)
- Seeds older than 30 days with `interview: pending`
- Ideas with no `strongest objection` filled in
- Contradictions between pages not yet surfaced
- Concepts mentioned in 3+ pages with no concept page
- Index entries pointing at missing files, or files missing from the index
- Ideas that look `mature` but haven't been extracted

Fix mechanical issues (index drift, missing back-links) directly. Propose, don't execute, anything that changes meaning. Commit `lint: <date>`.

### 6. Extract

Pull something out of the wiki into the world.

- **Output:** draft an essay, post, talk outline, BitDevs topic, or brief into `outputs/`, citing the idea pages it draws on. Mark source ideas `promoted` only once Justin ships it.
- **Action:** if an idea implies something to build or do, route it to the `idea-boardroom` skill for a verdict before anything goes to Linear. Record the verdict on the idea page.
- Commit `extract: <slug>`.

## Writing rules for wiki pages

- Plain, direct prose in Justin's register. No filler, no hedging.
- Never use the "it's not X, it's Y" construction.
- Lead each idea page with the one-sentence thesis.
- Keep idea pages under ~600 words. When one grows past that, it's probably two ideas: split and link.

## index.md format

One line per page, grouped by section, alphabetical within each:

```
- [[slug]] — one-line thesis · status · domains
```

## log.md format

Append-only, newest at the bottom:

```
## YYYY-MM-DD
- <op>: <slug> — one-line note
```
