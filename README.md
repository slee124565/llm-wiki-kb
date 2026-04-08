# llm-wiki-kb

一個適合個人或團隊使用的 LLM-friendly wiki starter repo。

這個 repo 的重點不是教你把一台 Mac 設成 agent workstation，而是示範如何把工作素材整理成可持續維護的知識庫。

## 這個 Repo 用來做什麼

當你想把工作素材變成之後還找得到、還能重用、還能持續改進的內容時，就可以用這個 repo：

- 文章
- 會議紀錄
- 截圖
- 逐字稿
- 重要觀察

核心想法很簡單：

1. 收集原始素材
2. 請 Claude 幫你整理
3. 把結果存成 wiki 頁面
4. 保持一個簡短的 `index.md` 和 `log.md`

## 你做什麼，Claude 做什麼

- 你負責收集原始素材
- Claude 幫你摘要、比較、串連觀念
- 你把整理後的結果存進 wiki
- 你偶爾回頭檢查 index 和 log

## Repo Structure

這個 starter repo 的最小骨架是：

- `raw/`
  放原始素材、未整理筆記、待處理來源
- `wiki/`
  放整理後的知識頁面
- `index.md`
  保持簡短的主題索引
- `log.md`
  記錄新增、修改與維護軌跡

這四個元素的重點不是檔案本身，而是讓你持續形成：

- capture
- compile
- link
- maintain

## 使用前先選路線

如果你只是想理解這個 repo 的 operating model，直接從這裡開始即可。

### 路線 A：你已經有自己的本機環境

這條路適合：

- 工程人員
- 已熟悉 Terminal / TUI 操作的人
- 已有自己的 Claude Code、Codex、Gemini CLI 或其他 agent 工作流的人

這種情況下，你可以直接 `git clone` 這個 repo，然後開始使用。

### 路線 B：你還不熟本機工具安裝

這條路適合：

- 非工程同仁
- 不熟 Terminal 的同仁
- 不知道 Claude Desktop、Claude Code、MCP、`gws` 應該怎麼接的人

如果你目前卡在這些問題：

- Terminal 基本操作
- Homebrew
- Node.js
- Claude Code CLI
- MCP setup
- Google Workspace `gws` CLI / MCP

請先看：

- [flh-claude-toolkit QUICKSTART](https://github.com/slee124565/flh-claude-toolkit/blob/main/QUICKSTART.md)

先用那份 quickstart 把工作站設好，再回來使用 `llm-wiki-kb`。

## 建議閱讀順序

先讀：

- [README.md](README.md)
- [ARCHITECTURE.md](ARCHITECTURE.md)
- [docs/ingest.md](docs/ingest.md)
- [docs/query.md](docs/query.md)
- [docs/lint.md](docs/lint.md)
- [docs/test-plan.md](docs/test-plan.md)

再看：

- [raw/README.md](raw/README.md)
- [wiki/README.md](wiki/README.md)

## 這個 Repo 的邊界

`llm-wiki-kb` 應聚焦在：

- knowledge base operating model
- repo shape
- ingest / query / maintenance workflow
- wiki page 與 index / log 的維護方式

`llm-wiki-kb` 不應長期承擔：

- 本機工具安裝教學
- CLI / MCP troubleshooting
- agent workstation rollout SOP

這些內容應導流到：

- [flh-claude-toolkit QUICKSTART](https://github.com/slee124565/flh-claude-toolkit/blob/main/QUICKSTART.md)

## 適合什麼情境

這個 repo 適合：

- 想建立個人 wiki
- 想讓團隊有一個輕量知識庫起點
- 想用 agent 協助整理與維護知識
- 想要一個比單純筆記工具更容易持續編譯與更新的 repo shape

## 不適合什麼情境

如果你當前的主要問題是：

- 工具還沒裝好
- Claude Desktop / Claude Code 不知道怎麼接
- `git`、`gws`、`node` 不知道先裝哪個
- MCP server 設定容易卡住

那你應先看：

- [flh-claude-toolkit QUICKSTART](https://github.com/slee124565/flh-claude-toolkit/blob/main/QUICKSTART.md)

先把工作站設好，再回來經營這個 wiki。

如果你的本機環境已經沒問題，則不需要先經過 `flh-claude-toolkit`。
