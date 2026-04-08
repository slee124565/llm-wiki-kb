# llm-wiki-kb

一個給非工程同仁使用的入門知識庫，適合在 Mac 上搭配 Claude Desktop App 建立個人或團隊 wiki。

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

- 你負責收集原始素材。
- Claude 幫你摘要、比較、串連觀念。
- 你把結果存進 wiki。
- 你偶爾回頭檢查 index 和 log。

如果你不熟悉終端機，也可以從這份 repo 開始。建議把工作環境分成兩層：

- `Claude Desktop App`
  主要 GUI 介面，適合日常問答、整理文件、使用 MCP 工具
- `Claude Code CLI`
  終端機中的 agent，適合安裝工具、檢查環境、修改檔案、執行 step-by-step setup

對非工程同仁來說，最實用的做法不是硬學 CLI 指令，而是先學會：

1. 打開 Terminal
2. 貼上一行指令
3. 看懂成功 / 失敗訊息
4. 必要時把結果貼回 Claude，讓 agent 繼續帶你做

## 公司 Rollout 版安裝順序

這個 repo 的公司預設 rollout 路徑，採用：

1. `Claude Desktop App`
2. `Node.js` local runtime
3. `Claude Code CLI`
4. `llm-wiki-kb` local repo
5. `Claude Code as MCP server`
6. `Google Workspace gws CLI`
7. `gws MCP server`

這條路徑的理由是：

- 先有 GUI，非工程同仁比較容易開始
- 先補本機 `Node.js`，後面很多 CLI / MCP 工具才有共同 runtime
- 先補 `Claude Code CLI`，讓後續多數安裝步驟都可以由 agent 協助完成
- 再補本地 repo，讓知識庫有固定落點
- terminal MCP 預設不走獨立 shell server，而是直接採 `Claude Code as MCP server`
- 最後才補 `gws`，把 Google Workspace 能力接進來

詳細步驟對應文件：

- [docs/mac-terminal-basics.md](docs/mac-terminal-basics.md)
- [docs/setup-homebrew.md](docs/setup-homebrew.md)
- [docs/setup-nodejs.md](docs/setup-nodejs.md)
- [docs/setup-github-gh-cli.md](docs/setup-github-gh-cli.md)
- [docs/setup-claude-code-cli.md](docs/setup-claude-code-cli.md)
- [docs/setup-terminal-mcp.md](docs/setup-terminal-mcp.md)
- [docs/setup-google-workspace-gws.md](docs/setup-google-workspace-gws.md)

## 公司 Rollout Checklist

### Stage 0: Terminal 基本操作

先完成：

- [docs/mac-terminal-basics.md](docs/mac-terminal-basics.md)

最小驗收：

- 知道怎麼打開 Terminal
- 知道怎麼貼上一行指令
- 知道怎麼把結果貼回 Claude

### Stage 1: Claude Desktop App

先到 [claude.ai](https://claude.ai) 安裝並登入 Mac 版 Claude Desktop App。

最小驗收：

- 可正常開啟 Claude Desktop App
- 已登入可用帳號

### Stage 2: 安裝 Node.js

先完成：

- [docs/setup-homebrew.md](docs/setup-homebrew.md)
- [docs/setup-nodejs.md](docs/setup-nodejs.md)

最小驗收：

- `node --version` 成功
- `npm --version` 成功
- `npx --version` 成功

這一步很重要，因為後面很多 CLI / MCP 工具都會依賴這台 Mac 本機先具備 Node.js 工具鏈。

### Stage 3: 安裝 Claude Code CLI

先完成：

- [docs/setup-claude-code-cli.md](docs/setup-claude-code-cli.md)

最小驗收：

- `claude --version` 成功
- `claude` 可以啟動
- `claude doctor` 可以跑完

簡易使用方式：

1. 在 Terminal 進入你想工作的資料夾
2. 執行：

```bash
claude
```

3. 直接輸入自然語言提示詞

第一次使用可以貼這段：

```text
請用繁體中文陪我完成接下來的安裝。
我對 Terminal 不熟，每次只給我一個步驟。
每一步都要先告訴我：
1. 我要貼哪一行指令
2. 成功時會看到什麼
3. 如果失敗要怎麼排查
等我貼出結果後，你再帶我做下一步。
```

### Stage 4: 安裝本地 repo

這一階段開始，建議直接讓 `Claude Code` 協助。

先完成：

- [docs/setup-homebrew.md](docs/setup-homebrew.md)
- [docs/setup-github-gh-cli.md](docs/setup-github-gh-cli.md)

在 Terminal 先啟動：

```bash
claude
```

再貼這段：

```text
請幫我在這台 Mac 上安裝或確認 GitHub `gh` CLI，然後把 `slee124565/llm-wiki-kb` clone 到本機。
我是非工程使用者，對 Terminal 不熟。

請一步一步帶我做：
1. 先檢查 `gh --version`
2. 如果沒有安裝，協助我安裝
3. 再幫我 clone repo
4. 最後幫我確認資料夾裡有 `raw/`、`wiki/`、`index.md`、`log.md`

每一步都只給我一個動作，等我貼結果後再往下。
```

完成後，再把這個資料夾加入 Claude Desktop App 的 Project。

最小驗收：

- `gh --version` 成功
- repo 已 clone 到本機
- Claude Desktop 已把此資料夾加入 Project

### Stage 5: 用 Claude Code 當 Terminal MCP

公司預設策略採這條，不預設開獨立 terminal server。

先完成：

- [docs/setup-terminal-mcp.md](docs/setup-terminal-mcp.md)

這一階段只採：

- `Claude Code as MCP server`

不採預設：

- 獨立 terminal MCP server

最小驗收：

- Claude Desktop 已讀到 `claude mcp serve` 提供的 MCP server
- 可以在 Claude Desktop 中請 Claude 檢查本地 repo 狀態

如果要讓 Claude Code 協助你完成這一步，先在 Terminal 執行：

```bash
claude
```

再貼這段：

```text
請幫我把 Claude Code 設定成 Claude Desktop 可用的 MCP server。
請先檢查 `claude --version`，再告訴我 Claude Desktop 的設定檔路徑。
之後請給我完整可貼上的 `claude_desktop_config.json` 範例，內容只先包含 `Claude Code as MCP server`。
等我貼出設定結果後，再幫我驗證下一步。
```

### Stage 6: 安裝 Google Workspace gws CLI

先完成：

- [docs/setup-homebrew.md](docs/setup-homebrew.md)
- [docs/setup-google-workspace-gws.md](docs/setup-google-workspace-gws.md)

最小驗收：

- `gws --version` 成功
- `gws auth login` 完成
- `gws drive files list --params '{"pageSize": 3}'` 可用

如果要讓 Claude Code 協助你完成這一步，先在 Terminal 執行：

```bash
claude
```

再貼這段：

```text
請幫我在這台 Mac 上安裝 Google Workspace `gws` CLI。
我是非工程使用者，對 Terminal 不熟。

請按以下順序一步一步帶我做：
1. 先檢查 `gws --version`
2. 如果未安裝，協助我安裝
3. 再帶我做 `gws auth login`
4. 最後幫我執行 `gws drive files list --params '{"pageSize": 3}'` 做驗收

每一步只給我一個動作，等我貼結果後再往下。
```

### Stage 7: 把 gws 接到 Claude Desktop

延續前一階段，把 `gws` MCP server 加到 `claude_desktop_config.json`。

最小驗收：

- Claude Desktop 可使用 `gws` MCP server
- 可以在 Claude Desktop 問到 Drive 或 Gmail 資料

如果要讓 Claude Code 協助你完成這一步，先在 Terminal 執行：

```bash
claude
```

再貼這段：

```text
請幫我把 `gws` MCP server 加到 Claude Desktop 的設定檔。
請先檢查我目前的 `claude_desktop_config.json` 是否已包含 `Claude Code as MCP server`。
如果沒有 `gws`，請給我一份完整、可直接貼上的 JSON，內容要同時包含：
1. `Claude Code as MCP server`
2. `gws` MCP server，先只開 `drive,gmail,calendar`

等我貼出設定結果後，再幫我做最小驗收。
```

## Agent-Assisted Rollout Prompt

如果你已經有 Claude、Codex 或 Gemini 等 agent 可以協助操作，直接貼這段：

```text
請先讀這個 repo 的 README：
https://github.com/slee124565/llm-wiki-kb/blob/main/README.md

我要依照這個 repo 的「公司 rollout 版安裝順序」完成 setup。
我是 Mac 上的非工程使用者，對 Terminal 不熟。

請用繁體中文一步一步帶我完成，嚴格依照下面順序，不要跳步：

1. Terminal 基本操作
2. Claude Desktop App 安裝與登入
3. 安裝 Claude Code CLI
4. clone `llm-wiki-kb` repo 並加入 Claude Desktop Project
5. 用 `Claude Code as MCP server` 接到 Claude Desktop
6. 安裝 Google Workspace `gws` CLI
7. 完成 `gws auth login`
8. 把 `gws` MCP server 接到 Claude Desktop
9. 最後做一次完整驗收

請遵守以下方式：
- 每一步先叫我執行一個檢查或安裝動作
- 等我貼出結果後，再進下一步
- 如果要改設定檔，請先告訴我路徑，再給我完整內容
- terminal MCP 預設只走 `Claude Code as MCP server`
- 如果有失敗，先排查再往下

每一步都要告訴我：
- 我要在哪裡按
- 要貼哪一行指令
- 成功時會看到什麼
- 失敗時該怎麼排查
```

### Claude Desktop App

先到 [claude.ai](https://claude.ai) 下載並安裝 Mac 版 Claude Desktop App，登入你的 Claude 帳號。

## 目錄結構

- `raw/`
  放原始素材，分成 `inbox/`、`sources/`、`assets/`。
- `wiki/`
  放整理過的知識頁，現在先以 `README.md` 和 `_template.md` 作為基礎。
- `index.md`
  簡短列出有哪些主題。
- `log.md`
  簡短記錄哪些內容有變動。
- `docs/`
  放穩定的使用說明。
- `CLAUDE.md`
  給 Claude Code 的操作規則。
- `ARCHITECTURE.md`
  說明這個 repo 的分層與 source of truth。
- `LICENSE`
  開源授權文件。

## 使用指南

### 1. 匯入 Google Drive 業務文件

把 Google Drive 裡跟業務相關的文件，先整理成可讀的素材，再放進 `raw/inbox/` 或 `raw/sources/`。

適合匯入的內容包括：

- 專案說明
- 會議紀錄
- 客戶簡報
- 需求文件
- 重要截圖

### 2. 請 Claude 整理成知識庫內容

你可以請 Claude 做這幾件事：

- 摘要重點
- 找出關鍵名詞
- 整理問題與答案
- 比較相似文件的差異
- 找出值得保留到 `wiki/` 的內容

整理好的結果，請存成 Markdown 放進 `wiki/`。

### 3. 更新 index 與 log

每次新增重要內容後，簡短更新：

- `index.md`：這個知識庫現在有哪些主題
- `log.md`：這次新增或修改了什麼

### 4. 用測試提示詞體驗查詢功能

當你已經匯入一些文件後，可以用這些提示詞測試 cowork 與知識庫查詢效果：

- `請幫我整理這些業務文件，說明目前最重要的三個重點。`
- `這些文件裡有沒有提到待辦事項、負責人、截止日？`
- `如果我要向主管報告，請幫我濃縮成 5 句話。`
- `這些文件之間有沒有重複、衝突或缺漏？`
- `根據目前資料，下一步我應該先問什麼問題？`

## 日常使用建議

建議把這個 repo 當成「本地工作資料庫」：

1. 先把一份素材放進 `raw/inbox/` 或 `raw/sources/`
2. 打開 Claude Desktop App，請它整理重點和後續問題
3. 把結果存成 Markdown 頁面，放進 `wiki/`
4. 在 `index.md` 和 `log.md` 各補一行

如果你已經裝好 `gws` CLI + MCP，還可以直接在 Claude Desktop 裡請 Claude：

- 幫你找 Google Drive 某份文件
- 幫你整理 Gmail thread 的重點
- 幫你從 Calendar / Drive / Gmail 回收可寫進 wiki 的內容

如果你已裝好 Claude Code CLI，還可以請 agent 協助：

- 檢查 repo 結構是否完整
- 幫你建立新 wiki 頁面
- 幫你更新 `index.md` 與 `log.md`
- 幫你驗證某個 setup 是否成功

## 閱讀順序

1. `README.md`
2. `CLAUDE.md`
3. `ARCHITECTURE.md`
4. `docs/README.md`
5. `wiki/README.md`
