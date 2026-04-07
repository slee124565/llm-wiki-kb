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
