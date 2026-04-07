# llm-wiki-kb

一個給非工程同仁使用的入門知識庫，適合在 Mac 上搭配 Claude App 建立個人或團隊 wiki。

## 這個 Repo 用來做什麼

當你想把工作素材變成之後還找得到、還能重用、還能持續改進的內容時，就可以用這個 repo：

- 文章
- 會議紀錄
- 截圖
- 逐字稿
- 重要觀察

核心想法很簡單：

1. 收集原始素材
2. 請 Claude App 幫你整理
3. 把結果存成 wiki 頁面
4. 保持一個簡短的 index 和 log，讓知識庫一直好用

## 你做什麼，Claude 做什麼

- 你負責收集原始素材。
- Claude 幫你摘要、比較、串連觀念。
- 你把結果存進 wiki。
- 你偶爾回頭檢查 index 和 log。

你不需要一開始就學 git、CLI，或複雜設定。

## 安裝與設定

### 快速安裝（已有 Claude App）

如果你已經安裝好 Claude Desktop App，可以直接把以下提示詞貼進 Claude Chat，讓 Claude 自動讀取這份說明文件、逐一確認環境狀態，並引導你完成所有設定步驟：

```
請從這個網址讀取安裝說明：
https://raw.githubusercontent.com/slee124565/llm-wiki-kb/main/README.md

讀完後，幫我逐步完成「安裝與設定」所有步驟。
每個步驟請先請我在終端機執行指令確認目前狀態，再決定是否需要安裝或設定：

1. 確認 gh CLI 是否已安裝（gh --version）
2. 確認 GitHub 帳號是否已登入（gh auth status）
3. 確認 llm-wiki-kb 是否已 clone 到本機；若尚未 clone，請引導我完成
4. 確認 Claude Desktop App 是否已將這個資料夾設定為 Project

每一步請用繁體中文說明，並等我回報結果後再進行下一步。
```

完成後，確保你可以在資料夾中看到 `raw/`、`wiki/`、`index.md` 和 `log.md`，並且 Claude Desktop App 已將它設定為 Project。

---

### 1. 安裝 Claude Desktop App

先到 [claude.ai](https://claude.ai) 下載並安裝 Mac 版 Claude Desktop App，並登入你的 Claude 帳號。

### 2. 用 Claude Chat 協助安裝 GitHub `gh` CLI 與設定帳號

如果你不熟悉終端機，可以直接在 Claude Chat 輸入：

> 幫我一步一步在 Mac 上用 Homebrew 安裝 GitHub `gh` CLI，並完成 GitHub 帳號登入。每一步都請寫得簡單一點。

完成後，確認你能在終端機執行 `gh --version`，以及可以順利登入 GitHub。

### 3. 用 Claude Chat 協助 clone 這個 repository，並設定成 Claude 的專案資料夾

接著請 Claude Chat 指導你把這個 repo clone 到 Mac 上，並在 Claude Desktop App 中把它設定為專案資料夾（Project），讓 Claude 之後能直接存取這個資料夾的內容。

你可以直接貼：

> 請幫我把以下 GitHub repository clone 到 Mac：https://github.com/slee124565/llm-wiki-kb
> clone 完成後，再教我怎麼在 Claude Desktop App 中把這個資料夾設定成 Project。請一步一步說明。

完成後，確保你可以在這個資料夾中看到 `raw/`、`wiki/`、`index.md` 和 `log.md`。

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

## 快速開始

1. 先把一份素材放進 `raw/inbox/` 或 `raw/sources/`。
2. 打開 Claude App，請它整理重點和後續問題。
3. 把結果存成 Markdown 頁面，放進 `wiki/`。
4. 在 `index.md` 和 `log.md` 各補一行。

## 閱讀順序

1. `README.md`
2. `CLAUDE.md`
3. `ARCHITECTURE.md`
4. `docs/README.md`
5. `wiki/README.md`
