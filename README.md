# llm-wiki-kb

An agent-friendly personal knowledge base starter for Claude App users on Mac.

This repo is built around a simple compounding loop:

1. capture raw sources
2. compile them into wiki pages
3. keep `index.md` and `log.md` updated
4. periodically lint and revise the knowledge base

## Repository Layout

- `raw/`
  Unmodified source material.
- `wiki/`
  Compiled knowledge pages written and maintained by the agent.
- `index.md`
  Content-oriented entry map for the wiki.
- `log.md`
  Chronological record of ingests, revisions, and checks.
- `docs/`
  Stable operating notes and workflows.

## Quick Start

1. Drop a source into `raw/inbox/` or `raw/sources/`.
2. Ask Claude App to extract the key claims, entities, and follow-up questions.
3. Save the result as a new or updated wiki page under `wiki/cards/` or `wiki/maps/`.
4. Update `index.md` and append a short entry to `log.md`.

## Reading Order

1. `CLAUDE.md`
2. `README.md`
3. `ARCHITECTURE.md`
4. `docs/README.md`
5. `wiki/README.md`

