# Mac Terminal Basics

這份文件給第一次接觸 Terminal 的使用者。

目標不是讓你變成工程師，而是讓你能安全地完成三件事：

1. 打開 Terminal
2. 貼上一行指令並執行
3. 把結果貼回 Claude 或其他 agent，讓它繼續帶你做

## 你會用到的觀念

- `Terminal`
  Mac 內建的文字介面，可以執行指令
- `Command`
  你貼進去的一行文字，例如 `gws --version`
- `Enter`
  貼完指令後按下去，電腦就會執行
- `Output`
  Terminal 顯示的結果，用來判斷成功或失敗

## 第一次打開 Terminal

1. 在 Mac 按 `Command + Space`
2. 輸入 `Terminal`
3. 按 Enter 打開

打開後你會看到一個可以輸入文字的畫面。

## 最基本操作

### 執行一行指令

1. 把指令完整複製
2. 在 Terminal 視窗點一下
3. 貼上指令
4. 按 Enter

### 看懂成功或失敗

通常有三種情況：

- 成功
  會看到版本號、清單、登入網址，或明確的 success 訊息
- 尚未安裝
  常見訊息像是 `command not found`
- 權限或設定不完整
  會看到 `not authenticated`、`permission denied`、`access blocked` 之類訊息

只要把完整訊息貼回 Claude，agent 通常就能接著判斷下一步。

### 中止目前指令

如果畫面卡住或你執行錯了，可以按：

```text
Control + C
```

## 這三個檢查指令最常用

### 檢查工具有沒有裝好

```bash
claude --version
gws --version
gh --version
```

### 看目前在哪個資料夾

```bash
pwd
```

### 看資料夾裡有哪些檔案

```bash
ls
```

## 什麼時候要停下來問 agent

遇到以下情況，不要自己亂猜，直接把畫面貼回 Claude 或其他 agent：

- 看不懂 Terminal 顯示什麼
- 指令跑很久沒有結束
- 跑出登入網址但不知道下一步
- 要你修改設定檔，不確定該貼什麼內容

## 推薦用法

對非工程同仁，最穩的用法是：

1. 先請 agent 給你一個步驟
2. 只執行那一個步驟
3. 把結果貼回去
4. 再做下一步

這樣比一次貼一大串命令安全很多。
