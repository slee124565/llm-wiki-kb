# ARCHITECTURE.md

This repo uses four layers:

- `raw/`
- `wiki/`
- `index.md`
- `log.md`

## 1. Raw Layer

`raw/` contains immutable source material:

- articles
- papers
- screenshots
- meeting notes
- imported transcripts

Sources are read by the agent but not rewritten in place.

## 2. Wiki Layer

`wiki/` contains the compiled knowledge base:

- `wiki/cards/`
  atomic knowledge pages
- `wiki/maps/`
  topic-level navigation pages

The wiki is the agent-owned compiled layer. It should reflect synthesis, not raw capture.

## 3. Index

`index.md` is a content-oriented entry map.

Its job is to answer:

- what topics exist
- which maps are stable
- which pages are useful entry points

It should stay thin.

## 4. Log

`log.md` is an append-only timeline.

Its job is to answer:

- what was ingested
- what was revised
- what was linted or checked

It should stay short and chronological.

## Optional Docs

`docs/` stores stable operating guidance:

- ingest workflow
- query workflow
- lint workflow
- maintenance notes

If a rule becomes stable enough to survive multiple sessions, it belongs in `docs/`, not in chat.

## Source of Truth

- Source facts live in `raw/`.
- Compiled understanding lives in `wiki/`.
- Navigation lives in `index.md`.
- History lives in `log.md`.

