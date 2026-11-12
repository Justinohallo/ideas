# Ideas

Justin's idea wiki. Raw thoughts go in, get interviewed, and compile into linked pages that accumulate over time. Politics, society, work, AI, Bitcoin, sports, anything.

A Domain OS built with the harness `wiki-tools` plugin: captures land in `wiki/_source/_inbox/`, Claude compiles them into `wiki/ideas/` and `wiki/concepts/`, and git is the source of truth. The full operating rules live in [CLAUDE.md](CLAUDE.md).

## How to use it

- **Capture:** paste or dictate a raw idea to Claude. It's committed immediately, untouched.
- **Interview:** Claude asks 5–8 questions to sharpen the claim, steelman the objection, and find connections. Now or later, your call.
- **Ask:** "what do I think about X?" or "where do my AI and politics ideas overlap?"
- **Lint:** "health check the ideas repo" runs `os-audit` plus idea checks: orphans, stale seeds, contradictions.
- **Extract:** turn mature ideas into essays, posts, talks, or send buildable ones through idea-boardroom.

Private repo. Keep it that way.
