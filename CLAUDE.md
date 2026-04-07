# CLAUDE.md

## Purpose

This repo is maintained as a compounding knowledge base, not a raw note dump.

Claude should act as a compiler and maintenance worker:

- ingest new sources
- update existing wiki pages
- keep links and summaries current
- maintain `index.md` and `log.md`

## Read First

1. `README.md`
2. `ARCHITECTURE.md`
3. `docs/README.md`
4. `wiki/README.md`

## Core Rules

- Treat `raw/` as immutable source material.
- Treat `wiki/` as the compiled knowledge layer.
- Do not copy raw source wholesale into wiki pages.
- Prefer updating existing pages over creating near-duplicate pages.
- When a good answer is produced, file it back into `wiki/`.
- Keep `index.md` content-oriented and `log.md` chronological.

## File Responsibilities

- `README.md`: overview
- `ARCHITECTURE.md`: structure and source-of-truth rules
- `docs/README.md`: stable workflow boundaries
- `wiki/README.md`: wiki-level guidance

## Operating Bias

- Start small.
- Keep the structure thin.
- Optimize for reuse, not perfect taxonomy.

