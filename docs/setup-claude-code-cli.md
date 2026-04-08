# Claude Code CLI Setup Guide

這份文件用來協助非工程同仁在 Mac 上安裝與使用 `Claude Code CLI`。

目的不是把你變成 CLI 重度使用者，而是讓你之後可以用 agent 協助完成：

- 安裝工具
- 檢查環境
- 修改本地 repo
- 做一步一步的 setup 與驗收

## 什麼時候需要 Claude Code CLI

如果你主要只想在 GUI 裡整理文件，`Claude Desktop App` 就夠用。

如果你希望 agent 幫你做更多本機操作，建議再安裝 `Claude Code CLI`：

- 檢查某個工具是否已安裝
- 幫你修改 Markdown 檔案
- 幫你驗證 repo 結構
- 幫你做更完整的 setup / repair workflow

## 官方前提

依 Anthropic 官方文件，Claude Code 需要：

- macOS 10.15+
- 網路連線
- Claude 帳號

官方安裝方式有兩種：

- `npm install -g @anthropic-ai/claude-code`
- `curl -fsSL https://claude.ai/install.sh | bash`

對第一次接觸 CLI 的 Mac 使用者，建議先用官方安裝 script。

## Step By Step 安裝

### 0. 打開 Terminal

先讀 [mac-terminal-basics.md](mac-terminal-basics.md)。

### 1. 檢查是否已安裝

在 Terminal 執行：

```bash
claude --version
```

如果有顯示版本號，代表已安裝，可以直接跳到「登入與第一次啟動」。

如果看到 `command not found`，繼續下一步。

### 2. 安裝 Claude Code CLI

執行官方安裝指令：

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

安裝完成後，再跑一次：

```bash
claude --version
```

### 3. 進入你的 repo

先切換到 `llm-wiki-kb` 的資料夾，例如：

```bash
cd ~/llm-wiki-kb
```

如果你不知道 repo 在哪裡，可以先在 Finder 找到資料夾，再把資料夾拖進 Terminal 視窗裡確認路徑。

### 4. 第一次啟動 Claude Code

執行：

```bash
claude
```

第一次啟動時，Claude Code 會要求你登入。

依畫面指示完成登入後，回到 Terminal。

### 5. 驗證安裝是否正常

執行：

```bash
claude doctor
```

如果看到健康檢查結果，代表環境大致正常。

## 最小使用方式

進入 repo 後，啟動：

```bash
claude
```

接著可以直接輸入自然語言，例如：

```text
請先讀 README.md、CLAUDE.md、ARCHITECTURE.md，告訴我這個 repo 的工作方式。
```

或：

```text
請幫我檢查這個 repo 是否缺少 index 或 log 更新。
```

## 適合初學者的 prompt

### 安裝後第一次使用

```text
請用繁體中文陪我熟悉 Claude Code。
先讀目前資料夾的 README.md 與 CLAUDE.md。
之後只教我三件事：
1. 怎麼請你檢查 repo
2. 怎麼請你修改 Markdown
3. 怎麼請你幫我驗證某個 setup 是否成功
每次只教一步。
```

### 請 agent 幫你做本機驗收

```text
請檢查這台 Mac 是否已具備 llm-wiki-kb 的基本工作環境。
請逐項檢查：
1. 目前資料夾是否正確
2. Claude Code 是否正常
3. Claude Desktop App 是否已可使用這個 repo
4. 如果已安裝 gws，是否能再告訴我下一步怎麼接到 Claude Desktop
請用繁體中文，一次只給我一個檢查步驟。
```

## 常見問題

### `claude: command not found`

代表尚未安裝，或安裝後 shell 還沒重新載入。先重新開一個 Terminal 視窗，再執行 `claude --version`。

### 登入後沒有反應

先關掉目前 Terminal 視窗，重新打開，再執行：

```bash
claude
```

### 不知道自己在哪個資料夾

執行：

```bash
pwd
```

## Agent-Assisted 安裝 Prompt

如果你已經有 Claude、Codex 或 Gemini 可以協助你，可以直接貼這段：

```text
我要在 Mac 上安裝 Claude Code CLI，但我對 Terminal 不熟。
請用繁體中文一步一步帶我完成，而且每一步都要：

1. 先叫我執行一個檢查指令
2. 等我貼結果後，再告訴我下一步
3. 告訴我成功時會看到什麼
4. 告訴我失敗時怎麼排查

目標是完成以下驗收：
- `claude --version` 成功
- `claude` 可以正常啟動
- `claude doctor` 可以跑完
- 我知道怎麼在 `llm-wiki-kb` repo 裡請你幫我做事情
```
