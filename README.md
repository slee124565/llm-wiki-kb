# llm-wiki-kb

An easy-start knowledge base for non-engineers who want to use Claude App on Mac to build a personal or team wiki.

## What This Repo Is For

Use this repo when you want to turn work material into something you can find again, reuse, and keep improving:

- articles
- meeting notes
- screenshots
- transcripts
- important observations

The main idea is simple:

1. collect raw material
2. ask Claude App to help you organize it
3. save the result as a wiki page
4. keep a short index and log so the knowledge base stays easy to use

## What You Do vs What Claude Does

- You collect the source material.
- Claude helps summarize, compare, and connect the ideas.
- You save the result into the wiki.
- You occasionally review the index and log.

You do not need to start with git, CLI, or a complex setup.

## Repository Layout

- `raw/`
  Store original material here.
- `wiki/`
  Store the cleaned-up knowledge pages here.
- `index.md`
  A short map of what topics exist.
- `log.md`
  A short timeline of what changed.
- `docs/`
  Stable instructions for how to use the repo.

## Quick Start

1. Put one item into `raw/inbox/` or `raw/sources/`.
2. Open Claude App and ask it to extract the main points and follow-up questions.
3. Save the answer as a Markdown page in `wiki/cards/` or `wiki/maps/`.
4. Add one line to `index.md` and one line to `log.md`.

## Reading Order

1. `README.md`
2. `CLAUDE.md`
3. `ARCHITECTURE.md`
4. `docs/README.md`
5. `wiki/README.md`
