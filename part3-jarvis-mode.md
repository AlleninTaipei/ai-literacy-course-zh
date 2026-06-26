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

# AI 啟動 JARVIS 模式 — 用 Claude Code 指揮真實工作

## Part 3 : Claude Code

> 不是學如何寫程式, 而是學會「指揮」AI 完成真實工作任務

---

### 3-1 CLAUDE.md

#### 工作資料夾根目錄只影響該專案

```markdown
# 工作環境說明

## 專案背景
公司週報與客戶簡報的製作資料夾.

## 輸出規範
- 預設語言: 繁體中文, 專業英文術語（需要時加括號標注）

## 禁止動作
- 不要刪除任何檔案
```

> 給 AI 的工作說明書, CLAUDE.md 是可以隨時修改的.

---

#### 全域 CLAUDE.md

Windows

```
C:\Users\<使用者名稱>\.claude\CLAUDE.md
```

Mac

```
~/.claude/CLAUDE.md
```

> 全域設定適合放「不管在哪個專案都成立」的規範.
> 專案級設定會覆蓋全域設定, 讓每個資料夾可以有自己的例外.

---

### 3-2 掌握你的夥伴正在做什麼

任務執行中, 對話區會出現類似這樣的文字:

格式是: 動作 (已花時間 · 消耗的 token 數量)

```
⠸ Reading… (8s · ↑2k tokens)
```

這代表 Claude Code 現在「正在讀取某個檔案」, 已經跑了 8 秒, 用了約 2,000 個 tokens.

#### 畫面底部: 狀態列

按 `Shift + Tab` 可循環切換三種執行模式:

| 模式 | 畫面顯示 | 說明 |
|-----|---------|------|
| 手動確認 | （無標示）| 每個操作都需要你逐一批准 |
| 自動模式 | `⏵⏵ auto mode on` | 所有操作自動執行, 不再詢問 |
| 接受編輯 | `⏵⏵ accept edits on` | 僅檔案編輯自動執行, 終端指令仍需確認 |

---

### 3-3 判斷原則

#### 時間數字持續增加、spinner 還在轉, 就代表它在跑

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

### 3-4 Commands and Skills

```
請幫我用 markdown 方式製表, 列出所有內建的 Commands 和它的功用說明, 轉存於桌面.
```

```
請幫我用 markdown 方式製表, 列出所有內建的 Skill 和它的功用說明, 轉存於桌面.
```

| 範圍 | Windows | Mac / Linux |
|-----|---------|-------------|
| 全域（所有專案） | `C:\Users\<名稱>\.claude\commands\` | `~/.claude/commands/` |
| 專案（只限當前） | `.claude\commands\`（放在資料夾根目錄） | `.claude/commands/` |

> 你可以請 Claude Code 把功能確認過的工作流程, 幫你寫成一個指令.

---

#### 動手做: 專案級 CLAUDE.md 範例

1. 開啟 [一天一AI — 文章摘要索引](https://github.com/AlleninTaipei/one_day_one_ai), 點擊右上角的 Fork
2. Fork 完成後, 網址會變成 `github.com/你的帳號/one_day_one_ai`, 這是你自己的副本
3. 點擊綠色的 Code 按鈕, 複製 HTTPS 網址
4. VS code 開啟資料夾 (你置放專案的資料夾)
5. 在終端機執行:

```bash
git clone https://github.com/你的帳號/one_day_one_ai.git
```

再開啟 `one_day_one_ai` 資料夾

`CLAUDE.md`: OpenAI 用戶請複製一份為 `AGENT.md`; Gemini 用戶請複製一份為 `GEMENI.md`

在終端機啟動 Claue code

```bash
請更新
```

---

### 3-5 工作流程範例

> Claude.ai 在瀏覽器裡運作, 碰不到你電腦的檔案系統.
> Claude Code 在你的電腦上運作, 可以讀、寫、移動、執行任何本地檔案.

---

#### 工作流程一: 批次掃描多檔、自動命名、同步更新彙整索引

```
掃描 recordings/ 資料夾內所有本週新增的 .txt 通話／會議錄音稿
對每一份檔案: 
1. 萃取通話日期與對象（客戶名稱或會議出席者）
2. 整理成: 決議事項（標注負責人）、待辦清單（按優先級）、待確認問題
3. 以 YYYYMMDD_meeting.md 命名, 存入 minutes/ 資料夾
4. 在 weekly_summary.md 最後追加一行摘要索引
```

#### 工作流程二: 掃描資料夾、重新命名、移動檔案

```
掃描 receipts/ 資料夾
把所有 .jpg 和 .pdf 的收據／發票: 
- 依日期重新命名為 YYYYMMDD_店家名稱
- 移入對應月份子資料夾（例如 2026-06/, 沒有就建立）
- 把總金額與明細彙整輸出到 monthly_expense.csv, 方便報稅或記帳
```

---

#### 工作流程三: 同時讀取多份本地檔案、交叉比對後生成

```
同時讀取 data/ 資料夾內的三份檔案: 
- this_month.csv（本月各平台實際收入: 蝦皮、官網、IG）
- last_month.csv（上月收入, 作對比）
- target.csv（自己設定的本月目標）

計算: 各平台達成率、與上月相比的成長或衰退幅度
生成一份 Marp 投影片, 給自己每月檢討用: 
- 6 頁, 每頁不超過 5 個重點, 自動帶入三份數據的對比數字
- 語氣: 給自己看的檢討報告, 誠實但不需要正式
- 存為 monthly_review.md
```

#### 工作流程四: 感知資料夾狀態、判斷哪些待處理、批次輸出

```
掃描 quotes/ 資料夾
找出所有符合以下條件的報價單: 
- 檔案修改時間超過 5 天
- 同資料夾內尚未存在對應的 follow_up_*.md

為每份報價單起草一封跟進信: 
- 表示理解, 不施壓; 簡要重申方案的兩個核心優勢
- 繁體中文, 200 字以內
- 存為 follow_up_YYYYMMDD_客戶名.md, 方便直接複製貼上寄出
```

---

#### 工作流程五: 比對時間戳、只補差異、追加更新現有檔案

```
讀取 index.md 的最後更新時間
掃描 notes/ 資料夾, 找出所有在此時間之後新增或修改的讀書／工作筆記 .md 檔案
對這些檔案: 
1. 萃取主題關鍵字
2. 將新條目追加至 index.md（不覆蓋現有條目）
3. 輸出變更摘要: 「本次新增 X 篇、更新 Y 個關鍵字索引」
```

>讀懂資料夾狀態、跨檔案比對、批次輸出, 這些都是在瀏覽器裡無法完成的動作.

---

### 3-6 核心工作模式

| Pattern | 概念 | 管理的重點 |
|---------|---------|------|
| Spec-first | 動手前先把需求寫下來 | 管理目標 |
| Atomic tasking | 一次只交辦一件事 | 管理複雜度 |
| Context engineering | 讓 AI 每次都知道背景 | 管理資訊 |
| Scaffold-and-fill | 先確認架構再填細節 | 管理流程 |
| Review-and-iterate | 像審稿一樣看 AI 的輸出 | 管理品質 |

> 與 AI 協作, 像是帶領一位能力很強但需要明確指引的數位助理.

---

### 3-7 完整對話示範

#### 多份產品規格 Excel 檔案彙整成一份

對話一（Spec-First）

```
只有一個 Worksheet tab 叫 Specifications.
A 欄位是空白; B1 是機種名稱; B2 往下是規格名稱（CPU、Chipset…）; C2 往下是對應說明.
並非每個 B 欄位都有資訊, 例如 B21 是 Memory, C21 到 C26 是它的說明, B22 到 B26 空白, B27 才是下一個規格名稱.
以上描述你是否了解 ?
```

在動手之前, 先把資料結構說清楚, 確保後續每一步都建立在正確的理解上.

對話二（Spec-First + Atomic Tasking）

```
有一堆這樣的 Excel 檔案, 一個檔案就是一個機種.
開一個新的 Excel 彙整所有機種: B1 = "Model", C1 = 機種名稱, 後續機種依序放 D、E… 欄.
困難在於每個舊檔案中, 相同規格佔的列數可能不一樣.

這個用 Python 可以做嗎 ? 以上描述你是否了解 ?
```

把「描述問題」和「請求執行」拆開成兩個步驟.

---

對話三（Scaffold-and-Fill）

```
請告訴我該把測試用的 Excel 舊檔案複製到哪個路徑.
請你檢視一下後, 再整理你的 actions.
```

讓 AI 說明它需要什麼（測試檔案放哪）、報告它打算怎麼做, 確認方向正確後再執行.

對話四（Context Engineering）

```
我想做到讓 PM 不需要安裝 Python 或其他任何套件, 只需要 consolidate_specs.exe 即可使用, 有方法嗎 ?
```

> 讓 AI 根據你的實際工作情境思考, 而不是給出通用答案.
> 在開始之前定義清楚（Spec-First）、一次只推進一件事（Atomic Tasking）、確認架構再執行（Scaffold-and-Fill）、提供使用者背景讓 AI 給出真正可用的答案（Context Engineering）.

---

### 3-8 AI 時代的數位資產

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
| CLAUDE.md | 全域 / 專案 - 讓 AI 認識你的工作環境; 持久化的工作規範與背景說明 |
| 執行中 | 讀懂動態指示器, 知道 AI 在做什麼; 還在動 ? 時間正常 ? 需要按鍵回應 ? |
| 權限系統 | 你的信任邊界, 由你決定 |
| Commands and Skills |  控制與擴充 Claude Code 的行為 |
| 工作流程範例 | 批次掃描自動命名 / 歸檔搬移檔案 / 跨檔比對生成 / 感知狀態批次輸出 / 增量比對追加更新 |
| Spec-first / Atomic / Context / Scaffold / Review | 任務性質、技術複雜度、開發動機都不同, 但驅動每一次有效協作的, 始終是同一套溝通節奏 |

---

> 恭喜你, 你已經學會了這個時代最重要的能力之一: 把意圖說清楚, 讓 AI 替你完成真實的工作.
> 從這裡開始, 每一次交辦, 都是你重新定義「工作」這兩個字的機會, 帶著你手邊正在進行的專案, 我們下次見面繼續討論.
