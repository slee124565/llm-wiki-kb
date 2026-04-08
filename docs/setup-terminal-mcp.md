# Terminal MCP Setup Guide

這份文件說明怎麼把「終端機能力」接進 Claude Desktop App。

先說結論：

- 如果你要的是最穩、最有官方背書的做法，優先用 `Claude Code as MCP server`
- 如果你真的需要一個獨立的 terminal MCP server，再考慮 `@modelcontextprotocol/server-terminal`

對非工程同仁，我建議預設只走第一條。

## 我選這條方案的理由

我這次先查了目前比較可信的來源：

- Anthropic 官方文件有明確寫到，可以把 `Claude Code` 當成 MCP server，接到 Claude Desktop
- OpenAI 官方目前有公開的是 Docs MCP，沒有看到官方 terminal MCP server
- MCP ecosystem 裡確實有 terminal 類 server，但多數是社群方案

其中 `@modelcontextprotocol/server-terminal` 這條，不是我找到的 Anthropic / OpenAI 官方明示推薦；這是我根據 MCP ecosystem 中可見的 package metadata、allowlist 能力與配置形式做的保守選擇。

所以如果你的目標是：

- 在 Claude Desktop 保持 GUI 友善
- 又希望有一部分本機操作能力
- 並且盡量降低安裝與安全風險

那麼最合理的第一選擇是：

- `claude mcp serve`

## 路線 A：推薦方案，用 Claude Code 當 Terminal MCP

這條路線的意思不是「直接把整個 shell 全開給 Claude」。

它的核心是：

- 先安裝 `Claude Code CLI`
- 再把 `Claude Code` 以 MCP server 方式接到 `Claude Desktop`
- 之後在 Claude Desktop 內，就能使用一部分 Claude Code 能力來協助本機工作

這是目前我最有信心推薦給非工程同仁的 terminal-like MCP 路徑。

### 前提

你需要先完成：

- [setup-claude-code-cli.md](setup-claude-code-cli.md)

### 1. 檢查 Claude Code 是否已安裝

在 Terminal 執行：

```bash
claude --version
```

如果有顯示版本號，繼續下一步。

### 2. 找到 Claude Desktop 設定檔

macOS 路徑：

```text
~/Library/Application Support/Claude/claude_desktop_config.json
```

### 3. 把 Claude Code MCP server 加進設定檔

加入這段：

```json
{
  "mcpServers": {
    "claude-code": {
      "type": "stdio",
      "command": "claude",
      "args": ["mcp", "serve"],
      "env": {}
    }
  }
}
```

如果你已經有別的 MCP server，例如 `gws`，就把它們一起放在同一個 `mcpServers` 物件裡。

例如：

```json
{
  "mcpServers": {
    "claude-code": {
      "type": "stdio",
      "command": "claude",
      "args": ["mcp", "serve"],
      "env": {}
    },
    "gws": {
      "command": "gws",
      "args": ["mcp", "-s", "drive,gmail,calendar"]
    }
  }
}
```

### 4. 完全關閉再重開 Claude Desktop App

只關視窗不夠，請完整退出後再重新打開。

### 5. 最小驗收

在 Claude Desktop 內測試：

```text
請檢查我目前這個 llm-wiki-kb repo 的結構，告訴我是否缺少 index 或 log 的更新。
```

或：

```text
請告訴我目前這個專案有哪些主要檔案，並說明 README、CLAUDE、ARCHITECTURE 的分工。
```

如果 Claude 可以正常使用 Claude Code 提供的能力，代表 MCP 接法基本成功。

### 這條方案適合什麼情境

- 非工程同仁第一次接觸 MCP
- 想讓 Claude Desktop 變得更能做本機工作
- 想保留 GUI 操作感，不想直接管理太多 shell server

## 路線 B：進階方案，用獨立 terminal MCP server

只有在你明確需要「讓 Claude 直接跑有限制的 shell 指令」時，再考慮這條。

我目前比較有信心的選項是：

- `@modelcontextprotocol/server-terminal`

原因：

- 名稱與 package scope 屬於 `@modelcontextprotocol`
- 設計上支援 `allowedCommands`
- 可以限制預設工作目錄與 timeout

但我要直接提醒：

- 這不是我會優先推薦給非工程同仁的第一條路
- 如果 allowlist 沒設好，風險會比 `Claude Code as MCP server` 高

### 適合使用的情況

- 你只想暴露少數 shell / npm 能力
- 你知道自己要開放哪些命令
- 你能接受這是比較進階、比較需要治理的配置

### 不適合使用的情況

- 使用者還不熟 Terminal
- 團隊沒有定義安全邊界
- 不確定哪些命令該開、哪些不該開

## Step By Step：安裝獨立 terminal MCP server

### 1. 先確認 `npx` 可用

執行：

```bash
npx --version
```

### 2. 建議先只開非常小的 allowlist

我建議第一版只開：

- `pwd`
- `ls`
- `cat`
- `echo`

如果是工作 repo 維護，再視需要補：

- `git`
- `npm`
- `node`

### 3. 把 terminal server 加進 Claude Desktop 設定檔

```json
{
  "mcpServers": {
    "terminal": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-terminal"],
      "config": {
        "allowedCommands": ["pwd", "ls", "cat", "echo", "git"],
        "defaultTimeout": 30000,
        "defaultCwd": "/Users/lee/ws/myBrainFood/publishes/llm-wiki-kb"
      }
    }
  }
}
```

如果 `defaultCwd` 要給同仁使用，應改成他自己的 repo 路徑，不要直接照抄別人的路徑。

### 4. 重開 Claude Desktop

修改設定檔後，完整退出再打開。

### 5. 最小驗收

在 Claude Desktop 測試：

```text
請只用 terminal 工具幫我列出目前資料夾有哪些檔案，並說明哪些是 onboarding guide。
```

## 安全建議

如果你真的要開獨立 terminal MCP，請至少遵守這些原則：

1. 不要一開始就開太多命令
2. 先限制在單一 repo 目錄
3. 不要把高風險命令放進 allowlist
4. 先用 read-only 心態測試，再逐步增加能力

高風險命令例如：

- `rm`
- `mv`
- `chmod`
- `sudo`
- `curl`

## 我對這兩條方案的建議

### 團隊 rollout 預設

請先用：

- `Claude Code as MCP server`

### 只有進階使用者才考慮

再加：

- `@modelcontextprotocol/server-terminal`

## Agent-Assisted 安裝 Prompt

如果你已經有 Claude、Codex 或 Gemini 可以協助你，可以貼這段：

```text
我要在 Mac 上為 Claude Desktop 設定 terminal MCP。
請先用最保守、最安全的方式帶我做。

請先判斷我應該走哪條路：
1. 優先用 Claude Code 作為 MCP server
2. 只有在我明確需要獨立 terminal MCP 時，才用 @modelcontextprotocol/server-terminal

我是非工程使用者，對 Terminal 不熟。
請用繁體中文一步一步帶我完成。

每一步都要：
- 先叫我執行一個檢查動作
- 等我回報結果再進下一步
- 如果要改設定檔，請先告訴我路徑，再給我完整 JSON
- 如果走獨立 terminal MCP，請幫我用最小 allowlist
```
