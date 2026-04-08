# Homebrew Setup Guide

這份文件用來協助非工程同仁在 Mac 上安裝 `Homebrew`。

很多 Mac 上常見的 CLI 工具都可以用 Homebrew 安裝，例如：

- `gh`
- `gws`
- `node`

如果你在 Terminal 看到：

```text
brew: command not found
```

通常就代表這台 Mac 還沒有安裝 Homebrew。

## 先做什麼檢查

打開 Terminal，執行：

```bash
brew --version
```

如果有顯示版本號，代表 Homebrew 已安裝。

如果看到 `command not found`，代表還沒裝好。

## 安裝前提

建議你先完成：

- [mac-terminal-basics.md](mac-terminal-basics.md)

## Step By Step 安裝

### 1. 檢查是否已安裝

執行：

```bash
brew --version
```

如果有版本號，就可以直接結束這份文件。

### 2. 執行官方安裝指令

在 Terminal 執行：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

安裝過程中，如果 Terminal 要你輸入密碼，請輸入你的 Mac 登入密碼。

畫面上不一定會顯示密碼字元，這是正常的。

### 3. 依畫面提示補上 shell 設定

安裝完成後，Homebrew 通常會在 Terminal 顯示一小段後續指令，請照畫面提示執行。

這一步很重要，因為它會把 `brew` 加進你的 shell path。

### 4. 重新打開 Terminal

請完全關掉目前的 Terminal 視窗，再重新打開。

### 5. 驗證安裝是否正常

執行：

```bash
brew --version
```

如果有版本號，代表 Homebrew 已可使用。

## 安裝成功後，下一步去哪裡

如果你接下來要：

- 安裝 Node.js：
  [setup-nodejs.md](setup-nodejs.md)
- 安裝 GitHub `gh` CLI：
  [setup-github-gh-cli.md](setup-github-gh-cli.md)
- 安裝 Google Workspace `gws` CLI：
  [setup-google-workspace-gws.md](setup-google-workspace-gws.md)

## 常見問題

### `brew: command not found`

代表 Homebrew 還沒安裝，或安裝後 shell path 還沒生效。

先關掉 Terminal，再重開一次，重新執行：

```bash
brew --version
```

如果還是不行，回頭確認你是否有執行安裝完成後畫面上顯示的 shell 設定指令。

### 安裝時卡很久

Homebrew 安裝需要下載檔案，可能會花一些時間。

如果超過很久都沒有新輸出，再把畫面貼回 agent。

### 不知道安裝後畫面要我做什麼

不要自己猜。

把安裝完成後 Terminal 顯示的最後幾行完整貼回 agent，請它告訴你哪一行需要再執行。

## Agent-Assisted 安裝 Prompt

如果你想讓 Claude、Codex 或其他 agent 帶你安裝，可以直接貼這段：

```text
請幫我在這台 Mac 上安裝 Homebrew。
我是非工程使用者，對 Terminal 不熟。

請用繁體中文一步一步帶我做，而且每一步都要：
1. 先叫我執行一個檢查
2. 告訴我成功時會看到什麼
3. 告訴我失敗時代表什麼
4. 等我貼結果後，再帶我做下一步

目標是完成以下驗收：
- `brew --version` 成功
- 我知道安裝完成後需要把哪一行 shell 設定貼進 Terminal
```
