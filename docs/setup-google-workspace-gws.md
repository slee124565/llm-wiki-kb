# Google Workspace gws CLI + MCP Setup Guide

這份文件用來協助非工程同仁在 Mac 上安裝 Google Workspace 官方團隊維護的 `gws` CLI，並把它接到 Claude Desktop App。

完成後，Claude Desktop App 可以透過 MCP 使用 Google Workspace 工具，例如：

- Google Drive
- Gmail
- Calendar
- Sheets
- Docs

## 這份 setup 的目的

對公司同仁來說，Google Workspace 是共通工作環境。

如果你只把文件下載到本機，Claude 當然還是可以整理，但你會少掉很多直接操作能力。裝好 `gws` 之後，agent 可以在權限範圍內幫你做更多事，例如：

- 找 Google Drive 文件
- 讀 Gmail thread
- 讀 Calendar 行程
- 協助把 Google Workspace 裡的內容回收到本地知識庫

## 官方前提

依 `googleworkspace/cli` 官方說明：

- 需要 Node.js 18+ 才能用 `npm install`
- 也可以直接用 GitHub Releases 的預編譯 binary
- macOS 可使用 Homebrew：`brew install googleworkspace-cli`
- OAuth 需要 Google Cloud project 與對應 credentials

官方 MCP 文件另外說明：

- Claude Desktop 的設定檔在 macOS 路徑是：
  `~/Library/Application Support/Claude/claude_desktop_config.json`
- `gws mcp` 可用 `-s` 指定要暴露哪些服務
- 建議從少量服務開始，避免超過 MCP client 的 tool limit

## 先決定你要走哪條登入路線

### 路線 A：公司已提供 OAuth client

這是最適合團隊 rollout 的方式。

你只需要：

1. 安裝 `gws`
2. 把公司提供的 OAuth client JSON 放到指定位置
3. 執行 `gws auth login`
4. 在瀏覽器登入你的公司帳號

### 路線 B：自己建立 OAuth 設定

這適合測試或個人 proof of concept。

你需要：

1. 有 Google Cloud project
2. 設定 OAuth consent screen
3. 建立 Desktop app client
4. 下載 `client_secret.json`
5. 執行 `gws auth login`

如果你只是想讓同仁快速上線，建議優先走路線 A，而不是讓每位同仁自己建一份 Google Cloud 設定。

## Step By Step 安裝

### 0. 打開 Terminal

先讀 [mac-terminal-basics.md](mac-terminal-basics.md)。

### 1. 檢查是否已安裝

執行：

```bash
gws --version
```

如果有顯示版本號，代表已安裝，可以跳到「登入」。

如果看到 `command not found`，繼續下一步。

### 2. 安裝 gws CLI

對多數 Mac 使用者，建議優先用 Homebrew：

```bash
brew install googleworkspace-cli
```

安裝後再檢查一次：

```bash
gws --version
```

如果你的電腦沒有 Homebrew，也可以請 agent 先帶你安裝 Homebrew，或改用官方 npm 安裝：

```bash
npm install -g @googleworkspace/cli
```

## Step By Step 登入

### 路線 A：公司已提供 OAuth client

1. 取得公司提供的 `client_secret.json`
2. 在 Terminal 建立設定資料夾：

```bash
mkdir -p ~/.config/gws
```

3. 把 `client_secret.json` 放到：

```text
~/.config/gws/client_secret.json
```

4. 執行登入：

```bash
gws auth login
```

5. 瀏覽器會開啟登入頁面，請使用你的公司 Google 帳號登入
6. 完成授權後，回到 Terminal

### 路線 B：自己建立 OAuth client

如果公司還沒有提供共用 OAuth client，請先完成這些步驟：

1. 到 Google Cloud Console 建立或選擇 project
2. 開啟 OAuth consent screen
3. App type 選 `External`
4. 把你自己的公司帳號加到 `Test users`
5. 建立一個 `Desktop app` OAuth client
6. 下載 JSON
7. 存到 `~/.config/gws/client_secret.json`
8. 執行：

```bash
gws auth login
```

如果你看到 `Access blocked`，通常是因為你沒有被加到 Test users。

## 驗證 gws 是否能正常使用

登入後，先跑一個最小測試：

```bash
gws drive files list --params '{"pageSize": 3}'
```

如果有回傳 JSON 結果，代表 `gws` 已經可以工作。

如果你目前只需要 Gmail，也可以請 agent 幫你用比較小範圍的 scope 重新登入。

## Step By Step 把 gws 接到 Claude Desktop App

### 1. 找到 Claude Desktop 設定檔

macOS 路徑：

```text
~/Library/Application Support/Claude/claude_desktop_config.json
```

如果檔案還不存在，可以建立一個新的。

### 2. 先決定要暴露哪些服務

官方文件建議從少量服務開始，避免工具太多。

對大多數知識庫 / 業務同仁，建議先從這個組合開始：

- `drive`
- `gmail`
- `calendar`

### 3. 寫入 MCP 設定

把設定檔改成這樣：

```json
{
  "mcpServers": {
    "gws": {
      "command": "gws",
      "args": ["mcp", "-s", "drive,gmail,calendar"]
    }
  }
}
```

如果你也想把 Claude Code 自己的工具一起接進 Claude Desktop，可以用：

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

如果 Claude Desktop 重開後找不到 `claude` 或 `gws`，先在 Terminal 執行：

```bash
which claude
which gws
```

再把設定檔裡的 `command` 改成完整路徑。

### 4. 完全關閉再重開 Claude Desktop App

設定檔修改後，請完全退出 Claude Desktop App，再重新打開。

### 5. 做最小驗收

在 Claude Desktop App 裡可以測試問：

```text
請列出我最近的 Google Drive 檔案，並告訴我哪些可能適合匯入 llm-wiki-kb。
```

或：

```text
請幫我整理今天 Gmail 最近幾封重要信件的重點。
```

## 建議的服務範圍

先從小範圍開始，不要一開始就用 `all`。

- 輕量版：`drive,gmail`
- 平衡版：`drive,gmail,calendar`
- 進階版：`drive,gmail,calendar,sheets,docs`

## Agent-Assisted 安裝 Prompt

如果你已經有 Claude、Codex 或 Gemini 可以協助你，可以直接貼這段：

```text
我要在 Mac 上安裝 Google Workspace 的 gws CLI，並把它接到 Claude Desktop App。
我對 Terminal 不熟，請用繁體中文一步一步帶我做。

請遵守以下方式：
1. 每一步先叫我執行一個檢查或安裝指令
2. 等我貼出結果後，再告訴我下一步
3. 如果要修改設定檔，請先告訴我檔案路徑、再給我完整內容
4. 優先使用最少服務數量的 MCP 設定，不要一開始就暴露全部工具

我的驗收目標是：
- `gws --version` 成功
- `gws auth login` 完成
- `gws drive files list --params '{"pageSize": 3}'` 可用
- Claude Desktop App 已加入 `gws` MCP server
- 我可以在 Claude Desktop 裡問到 Drive 或 Gmail 資料
```

## 常見問題

### `gws: command not found`

代表尚未安裝完成，或 shell 沒有重新載入。先關掉 Terminal，再開一個新的視窗測試 `gws --version`。

### `Access blocked`

通常代表 OAuth consent screen 沒有把你加到 Test users，或公司提供的 OAuth client 還沒設定好。

### Claude Desktop 裡看不到工具

先檢查三件事：

1. `claude_desktop_config.json` 格式是否正確
2. `gws` 指令在 Terminal 是否能正常執行
3. Claude Desktop App 是否有完全重開
