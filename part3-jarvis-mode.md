--- 
marp: true
theme: default
backgroundColor: #1A1A1A
color: #F5F0E8
paginate: true
---

<style>
section {
  font-size: 24px;
}
table {
  border-collapse: collapse;
}
th {
  background-color: #D97757;
  color: white;
}
td {
  background-color: #1A1A1A;
}
blockquote {
  background-color: #1A1A1A;
  border-left: 8px solid #D97757;
  padding: 1.5rem;
  border-radius: 4px;
  font-style: italic;
  color: #F5E0E8;
}
</style>

# 啟動 JARVIS 模式 — 指揮 AI Agent

## Part 3 : Claude Code

> 不是學如何寫程式, 而是學會「指揮」AI 完成真實工作任務

---

### 3-1 掌握你的夥伴正在做什麼

#### 動手做: 開啟 Part 2 那個 `one_day_one_ai` 資料夾

`CLAUDE.md`: OpenAI 用戶請複製一份為 `AGENT.md`; Gemini 用戶請複製一份為 `GEMENI.md`

在終端機啟動 Claude Code

```bash
請更新
```

任務執行中, 對話區會出現類似這樣的文字:

格式是: 動作 (已花時間 · 消耗的 token 數量)

```
⠸ Reading… (8s · ↑2k tokens)
```

這代表 Claude Code 現在「正在讀取某個檔案」, 已經跑了 8 秒, 用了約 2,000 個 tokens.

---

#### 畫面底部: 狀態列

按 `Shift + Tab` 可循環切換三種執行模式:

| 模式 | 畫面顯示 | 說明 |
|-----|---------|------|
| 手動確認 | （無標示）| 每個操作都需要你逐一批准 |
| 自動模式 | `⏵⏵ auto mode on` | 所有操作自動執行, 不再詢問 |
| 接受編輯 | `⏵⏵ accept edits on` | 僅檔案編輯自動執行, 終端指令仍需確認 |

> Claude Code 的設計哲學是「人始終在決策圈內」.
> 在做重大決策前會停下來確認, 你設定的信任邊界, 決定了它能自主行動的範圍.

---

### 3-2 判斷原則

#### 時間數字持續增加, 就代表它在跑

```
Claude Code wants to execute a bash command:
  git push origin main

1. Yes
2. Yes, always
3. No
```

| 選項 | 意義 | 適合時機 |
|-----|------|---------|
| Yes（本次同意）| 這次允許, 下次再問 | 第一次嘗試某個操作 |
| Yes, always（永遠同意）| 這類操作以後不再詢問 | 你已確認這個操作安全 |
| No（拒絕）| 不執行, Claude Code 會尋找替代方案 | 不確定這個操作是否正確 |

---

### 3-3 CLAUDE.md, Commands and Skills

- CLAUDE.md 是給 AI 的工作手冊, 每次對話開始都會被讀取
- Commands 要使用者明確輸入 `/xxx` 才會執行; Skills 預設由 Claude 依任務內容自主判斷是否調用, 也可以用 `/skill-name` 手動觸發
- 這門課用的 CLAUDE.md 已經把 Skills 的自動調用關掉, 改成一律要靠 slash command 明確發起
- 全域 CLAUDE.md 適合放「不管在哪個專案都成立」的規範
- 專案級 CLAUDE.md 會疊加在全域規則之上, 讓每個資料夾可以再補上自己的例外, 不是取代全域規則

```
/help
```

```
/code-review           ← Command, 要明確輸入才會執行
"請幫我做資料視覺化"     ← 符合某個 Skill 的描述, Claude 可能自主調用
```

---

### 3-4 Claude Code 能做什麼

| 能力 | 說明 |
|------|------|
| 讀取整個專案 | 掃描資料夾結構, 理解各檔案的關聯與脈絡 |
| 讀寫任意檔案 | 直接建立、修改、刪除工作目錄中的文件 |
| 執行系統指令 | 安裝工具、處理檔案、呼叫外部服務 |
| 搜尋整個資料夾 | 用關鍵字在所有文件中找到相關內容 |
| 多步驟任務規劃 | 把複雜任務拆解成子步驟, 逐步執行並回報進度 |
| Git 整合 | 讀取差異、撰寫 commit 訊息、管理分支 |

> Claude.ai 在瀏覽器裡運作, 碰不到你電腦的檔案系統.
> Claude Code 在你的電腦上運作, 可以讀、寫、移動、執行任何本地檔案.

---

### 3-5 核心工作模式

| Pattern | 概念 | 管理的重點 |
|---------|---------|------|
| Spec-first | 動手前先把需求寫下來 | 管理目標 |
| Atomic tasking | 一次只交辦一件事 | 管理複雜度 |
| Context engineering | 讓 AI 每次都知道背景 | 管理資訊 |
| Scaffold-and-fill | 先確認架構再填細節 | 管理流程 |
| Review-and-iterate | 像審稿一樣看 AI 的輸出 | 管理品質 |

---

### 3-6 AI 時代的數位資產

| 類型          | AI-Assisted Development          | AI-Native Assets                 |
| ----------- | --------------------- | ---------------------------- |
| AI 扮演角色     | Developer             |  Agent              |
| 最終交付        | 可執行工具 (exe、網站、Script) | Workflow、Agent   |
| 使用者需要 AI 嗎？ | 不需要                   | 需要                           |
| 更新方式        | 作者重新發布版本              | 使用者重新執行 AI                   |
| 擴充性         | 功能固定                  | 可持續演化                        |
| 適合對象        | 全公司、RD、PM、Sales、行政       | 開發者（具備 Agentic Coding Environment） |

---

## 小結: Part 3 概念關係總覽

| 主題 | 說明 |
|-----|-------|
| 執行中 | 讀懂動態指示器（⠸ Reading… · 時間 · tokens）; Shift + Tab 切換手動確認 / 自動模式 / 接受編輯 |
| 判斷原則 | Yes 本次同意 / Yes, always 永遠同意 / No 拒絕; 你設定的信任邊界, 決定了 AI 能自主行動的範圍 |
| CLAUDE.md / Commands / Skills | 全域 CLAUDE.md 適合所有專案共用的規範, 專案級規則疊加補充而非覆蓋; Commands 要明確輸入才執行, Skills 預設可由 Claude 自主調用 |
| Claude Code 能做什麼 | 讀取專案、讀寫檔案、執行指令、搜尋資料夾、多步驟任務規劃、Git 整合; 直接在本機檔案系統工作, 不是瀏覽器裡的聊天視窗 |
| 核心工作模式 | Spec-first / Atomic tasking / Context engineering / Scaffold-and-fill / Review-and-iterate; 始終是同一套溝通節奏 |
| AI 時代的數位資產 | AI-Assisted Development（AI 是 Developer, 交付可執行工具）vs AI-Native Assets（AI 是 Agent, 交付 Workflow / Agent）|

---

> 恭喜你, 你已經學會了這個時代最重要的能力之一: 把意圖說清楚, 讓 AI 替你完成真實的工作.
