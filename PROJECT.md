# Ideas Wiki

**Status:** Intake complete · 2026-11-12 · Next: first capture + interview (no architect phase needed)
**Client:** Internal
**Type:** Knowledge project (LLM Wiki pattern, markdown + git)
**Phase:** Greenfield
**Parent:** Digital Twin / Claude Harness

---

## Problem Statement

Ideas across politics, society, work, AI, Bitcoin and sports surface in random chats, walks and conversations, then evaporate. There's no single place where a raw idea gets captured, pressure-tested, and compounded over time so it can later be pulled out as an essay, talk, product, or decision.

---

## Success Criteria

| Metric | Target | Notes |
|--------|--------|-------|
| Capture latency | Raw idea committed in under 1 minute from dump | Capture never waits on interview |
| Interview coverage | 80%+ of seeds interviewed within 14 days | Lint flags anything older |
| Extraction | 1+ idea promoted per month (output or boardroom verdict) | [ASSUMED: target — confirm] Proves the repo isn't a graveyard |
| Link density | Every idea page links to at least 1 other page after 10 ideas exist | Cross-domain value depends on it |

**Done when:** ongoing area. Health is judged by the monthly lint, not a finish line.

---

## Stakeholders

| Role | Name | Responsibilities |
|------|------|------------------|
| Owner / only author | Justin | Captures, answers interviews, decides what gets extracted |
| Maintainer | Claude | Writes and maintains `wiki/`, `index.md`, `log.md` per CLAUDE.md |
| Downstream | idea-boardroom → Linear; Bitcoin Builder / BitDevs content; Burrard Works writing | Consume promoted ideas |

---

## Scope

### In Scope (Phase 1)

- Repo `Justinohallo/ideas` (private), scaffolded as a Domain OS with harness `wiki-tools` (os-init)
- Six operations: capture, interview, ingest, query, lint, extract (see CLAUDE.md)
- Capture from the claude.ai Project "Ideas" into `wiki/_source/_inbox/`

### Explicitly Out of Scope

- A web UI or Next.js viewer (the workshop-app stack). Add later only if reading the repo on GitHub/Obsidian proves painful.
- Daily journaling, task tracking, client work — those belong to Digital Twin, Linear and client repos respectively.
- Public publishing from this repo. Outputs are drafts; publishing happens elsewhere.

### MVP vs. Full Build

MVP is the repo as scaffolded plus a capture surface. Full build would add a scheduled monthly lint and possibly an MCP or Project-based capture shortcut from mobile.

---

## Tech Stack & Constraints

| Layer | Decision | Rationale |
|-------|----------|-----------|
| Storage | Markdown in git | Diffable history of how ideas evolve; LLM Wiki pattern |
| Hosting | GitHub, private | Political/personal content |
| Maintainer | Claude via this session or Claude Code | Reads CLAUDE.md as schema |
| Viewer | GitHub web / Obsidian (optional) | No custom UI in Phase 1 |

**Hard constraints:**
- Repo stays private. No secondary remotes.
- `wiki/_source/` is immutable.

---

## Open Questions

- [ ] Boundary with Digital Twin `journal/`: a passing thought in a journal entry, does it get copied here, or only things Justin explicitly flags as ideas? (Justin)
- [ ] Monthly lint as a scheduled task, or on demand only? (Justin)

---

## Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| Capture graveyard: ideas go in, nothing comes out | High | High | Extraction metric, monthly lint flags mature-but-unextracted ideas |
| Interview friction suppresses capture | Medium | High | Capture commits first; interview deferrable (`interview: pending`) |
| Overlap with Digital Twin journal / idea-boardroom creates three homes for an idea | Medium | Medium | Scope boundary above; boardroom only via Extract |
| Intake/lint flagged but never run (known Digital Twin failure mode) | Medium | Medium | Scheduled lint if confirmed; lint output lists the exact next action |

---

## Downstream

**Recommended next step:** none from the pipeline. This is a knowledge project; CLAUDE.md is already the spec. Next action is the first real capture.
