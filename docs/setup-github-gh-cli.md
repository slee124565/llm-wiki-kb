# GitHub gh CLI Setup Guide

這份文件用來協助非工程同仁在 Mac 上安裝 GitHub 官方的 `gh` CLI。

在這個 repo 的 rollout 流程裡，`gh` 最常用在兩件事：

- 把 `llm-wiki-kb` clone 到本機
- 讓 agent 幫你檢查 GitHub repo 或 pull request 相關資訊

## 先做什麼檢查

先打開 Terminal，執行：

```bash
gh --version
```

如果有顯示版本號，代表 `gh` 已安裝。

如果看到 `command not found`，代表還沒裝好。

## 安裝前提

建議你先完成：

- [mac-terminal-basics.md](mac-terminal-basics.md)

如果你前面已經裝好 Node.js，也很好，但 `gh` 不一定依賴 Node.js 才能安裝。

## 建議安裝方式

對大多數 Mac 使用者，建議優先用 Homebrew 安裝：

```bash
brew install gh
```

如果你的 Mac 還沒有 Homebrew，就先把錯誤訊息貼回 agent，請它帶你補安裝。

如果你的電腦還沒有 Homebrew，先看：

- [setup-homebrew.md](setup-homebrew.md)

## Step By Step 安裝

### 1. 檢查是否已安裝

執行：

```bash
gh --version
```

如果有版本號，就可以直接跳到後面的登入或 clone repo。

### 2. 安裝 `gh`

執行：

```bash
brew install gh
```

安裝完成後，請再檢查一次：

```bash
gh --version
```

### 3. 視需要登入 GitHub

如果你只是要 clone 公開 repo，不一定要先登入。

如果你後面要：

- 存取 private repo
- 在本機用 `gh` 做更多 GitHub 操作

可以執行：

```bash
gh auth login
```

依畫面選擇：

- GitHub.com
- HTTPS
- Login with a web browser

接著照瀏覽器指示完成登入。

### 4. 最小驗收

至少確認：

```bash
gh --version
```

如果你已經登入，也可以再檢查：

```bash
gh auth status
```

## 用 `gh` clone `llm-wiki-kb`

如果你要把這個 repo 抓到本機，可以執行：

```bash
gh repo clone slee124565/llm-wiki-kb
```

完成後，進入資料夾：

```bash
cd llm-wiki-kb
ls
```

你應該至少會看到：

- `raw`
- `wiki`
- `index.md`
- `log.md`

## 常見問題

### `gh: command not found`

代表 `gh` 還沒安裝，或安裝後 Terminal 還沒重新載入。

先重新打開一個 Terminal 視窗，再執行：

```bash
gh --version
```

### `brew: command not found`

代表這台 Mac 還沒有 Homebrew。

這時不要自己亂找安裝方式，直接把錯誤訊息貼回 agent，請它一步一步帶你安裝 Homebrew，再回來裝 `gh`。

### `gh auth status` 顯示未登入

如果你只是 clone 公開 repo，可以先略過。

如果你需要 private repo 或更完整的 GitHub 操作，再執行：

```bash
gh auth login
```

### `gh repo clone` 失敗

先把完整錯誤訊息貼回 agent。

常見原因包括：

- 網路問題
- 尚未登入但目標 repo 不是公開的
- repo 名稱打錯

## Agent-Assisted 安裝 Prompt

如果你想讓 Claude、Codex 或其他 agent 帶你安裝，可以直接貼這段：

```text
請幫我在這台 Mac 上安裝 GitHub `gh` CLI，並確認我可以用它 clone `slee124565/llm-wiki-kb`。
我是非工程使用者，對 Terminal 不熟。

請用繁體中文一步一步帶我做，而且每一步都要：
1. 先叫我執行一個檢查
2. 告訴我成功時會看到什麼
3. 告訴我失敗時代表什麼
4. 等我貼結果後，再帶我做下一步

目標是完成以下驗收：
- `gh --version` 成功
- 如果需要，`gh auth login` 可完成
- `gh repo clone slee124565/llm-wiki-kb` 成功
```
