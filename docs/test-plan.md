# Test Plan

This document defines how to verify that `llm-wiki-kb` works well when used by a Claude agent.

## Purpose

Verify that the repo supports a Claude-driven workflow for:

- importing raw business materials
- turning sources into reusable wiki pages
- keeping `index.md` and `log.md` current
- answering follow-up questions from the compiled wiki
- avoiding source contamination and duplicate pages

## Scope

In scope:

- `raw/`
- `wiki/`
- `index.md`
- `log.md`
- `docs/`
- `CLAUDE.md`
- `ARCHITECTURE.md`

Out of scope:

- deep GitHub automation
- custom scripts beyond normal file editing
- external integrations that are not documented in this repo

## Test Environment

- Mac
- Claude Desktop App installed and signed in
- GitHub account available
- `gh` CLI installed and authenticated
- This repository cloned locally and used as the Claude cowork project root

## Success Criteria

The repo is considered healthy when Claude can:

1. read the repo guidance correctly
2. place raw material in the right layer
3. synthesize source material into wiki content
4. update navigation and history without drifting
5. answer questions from the compiled knowledge instead of re-reading raw sources each time

## Test Cases

| ID | Scenario | Input | Expected Result |
| --- | --- | --- | --- |
| TP-01 | Bootstrap repo understanding | Ask Claude to explain the repo structure after reading `README.md`, `CLAUDE.md`, and `ARCHITECTURE.md` | Claude describes `raw/`, `wiki/`, `index.md`, and `log.md` correctly and does not invent missing folders |
| TP-02 | Raw source import | Provide a new article, memo, or transcript and ask Claude to place it in the repo | Source is stored in `raw/` and is not rewritten into a synthesized page |
| TP-03 | Wiki synthesis | Ask Claude to turn imported source material into a reusable note | Claude creates or updates a page in `wiki/` that contains synthesis, not copy-paste text |
| TP-04 | Update existing page | Provide a second source that changes or refines an earlier conclusion | Claude updates the existing wiki page instead of creating a near-duplicate |
| TP-05 | Index maintenance | Add a new topic or wiki page and ask Claude to maintain navigation | `index.md` gains a thin entry that points to the new topic or page |
| TP-06 | Log maintenance | Perform an ingest or revision task and ask Claude to record what changed | `log.md` gets a short chronological entry with the key action |
| TP-07 | Query from wiki | Ask a practical question that should be answered from the compiled knowledge | Claude answers from wiki-level synthesis and not only from raw source replay |
| TP-08 | Conflict detection | Provide two sources that disagree | Claude highlights the conflict and does not silently merge them |
| TP-09 | Duplicate control | Ask Claude to add a topic that already exists | Claude reuses or updates the existing structure rather than creating a duplicate page |
| TP-10 | Lint behavior | Ask Claude to check for missing links, stale entries, or orphan pages | Claude identifies issues and proposes focused cleanup actions |

## Suggested Prompt Set

Use these prompts during manual verification:

- `請先讀這個 repo 的 README、CLAUDE、ARCHITECTURE，並告訴我你理解的工作方式。`
- `我有一份新的業務文件，請幫我放到正確的 raw 層，並說明下一步怎麼整理。`
- `請把這些來源整理成一份可以重複使用的 wiki 筆記。`
- `這份新資料跟舊結論有衝突嗎？如果有，請更新既有頁面。`
- `請幫我更新 index 和 log，讓我之後找得到這個主題。`
- `根據目前 wiki，回答我這個業務問題。`

## Pass / Fail Rules

- Pass if Claude keeps raw material and compiled knowledge separated.
- Pass if Claude prefers updating existing pages over duplicating them.
- Pass if `index.md` stays thin and `log.md` stays chronological.
- Fail if Claude copies raw material wholesale into wiki pages.
- Fail if Claude ignores repo guidance and invents new structure.
- Fail if navigation and history are not updated after significant changes.
