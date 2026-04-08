# Node.js Setup Guide

這份文件用來協助非工程同仁在 Mac 上先補好 `Node.js` 環境。

很多你後面會用到的工具，都不是單靠 Claude Desktop App 就能工作，還需要這台 Mac 本機先有：

- `node`
- `npm`
- `npx`

常見會依賴這組工具的情況：

- 安裝 `Claude Code CLI`
- 使用 `npm install -g ...` 安裝 CLI
- 執行 `npx ...` 類型的工具
- 某些 MCP server 或 CLI 需要 Node.js runtime

## 先做什麼檢查

先打開 Terminal，再執行：

```bash
node --version
npm --version
npx --version
```

如果三個都有版本號，代表這台 Mac 已具備基本 Node.js 工具，可以直接往下一份 setup 文件走。

如果看到 `command not found`，就代表還沒裝好。

## 建議安裝方式

對非工程同仁，最容易理解的做法是：

1. 直接安裝 Node.js 官方提供的 Mac installer
2. 安裝完成後重新打開 Terminal
3. 再重新跑一次版本檢查

建議選擇：

- `LTS` 版本

因為大多數 CLI / MCP 工具都會優先支援穩定版，而不是最新 experimental 版本。

## Step By Step 安裝

### 0. 先熟悉 Terminal

如果你還不熟 Terminal，先看：

- [mac-terminal-basics.md](mac-terminal-basics.md)

### 1. 檢查是否已安裝

執行：

```bash
node --version
npm --version
npx --version
```

如果都有版本號，可以直接結束這份文件。

### 2. 安裝 Node.js

請用瀏覽器打開 Node.js 官方網站，下載 Mac 版 `LTS` installer。

安裝完成後，請：

1. 完全關掉目前的 Terminal 視窗
2. 重新打開 Terminal
3. 再執行一次版本檢查

### 3. 驗證安裝是否正常

執行：

```bash
node --version
npm --version
npx --version
```

你至少應該看到三個版本號。

## 如果你偏好 Homebrew

如果你的 Mac 已經有 Homebrew，也可以請 agent 帶你用 Homebrew 安裝 Node.js。

但對第一次接觸 Terminal 的使用者，官方 installer 通常更直觀。

如果你的電腦還沒有 Homebrew，先看：

- [setup-homebrew.md](setup-homebrew.md)

## 安裝成功後，下一步去哪裡

如果你接下來要：

- 安裝 Claude Code CLI：
  [setup-claude-code-cli.md](setup-claude-code-cli.md)
- 安裝 Google Workspace `gws` CLI：
  [setup-google-workspace-gws.md](setup-google-workspace-gws.md)
- 設定 terminal / MCP 相關工具：
  [setup-terminal-mcp.md](setup-terminal-mcp.md)

## 常見問題

### `node: command not found`

代表 Node.js 還沒裝好，或安裝後 Terminal 還沒重新打開。

先完全關掉 Terminal，再重開一次，重新執行：

```bash
node --version
```

### `npm: command not found`

通常代表 Node.js 沒有完整安裝成功。

請重新檢查：

```bash
node --version
```

如果 `node` 有、`npm` 沒有，建議重新安裝一次 Node.js。

### `npx: command not found`

這通常表示本機 Node.js 工具鏈不完整，或版本太舊。

先重新檢查：

```bash
node --version
npm --version
```

如果還是不行，把完整錯誤訊息貼回 agent，請它帶你排查。

## Agent-Assisted 安裝 Prompt

如果你想讓 Claude、Codex 或其他 agent 一步一步帶你安裝，可以直接貼這段：

```text
我要先把這台 Mac 的 Node.js 環境裝好，因為後面還要裝 Claude Code CLI 與其他 Node 工具。
我是非工程使用者，對 Terminal 不熟。

請用繁體中文一步一步帶我完成，而且每一步都要：
1. 先叫我執行一個檢查
2. 告訴我成功時會看到什麼
3. 告訴我失敗時代表什麼
4. 等我貼結果後，再帶我做下一步

目標是完成以下驗收：
- `node --version` 成功
- `npm --version` 成功
- `npx --version` 成功
```
