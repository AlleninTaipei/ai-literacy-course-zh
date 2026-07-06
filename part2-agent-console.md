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

# 個人電腦新情境 — 從文書處理機到 Agent 控制台

## Part 2 : 什麼是 Agent ？

> 以前, 電腦是你的工具.
> 現在, 電腦是你的辦公室, 而 AI Agent, 是在裡面替你工作的員工.

[LLM Agent Stack](llm-agent-stack.html)

---

### 2-1 Claude Code

如果 ChatGPT 是你的電話顧問, 你打過去問, 它給建議, 但它看不到你桌上的東西、也不能幫你動手
那麼 Claude Code 就是坐在你旁邊的同事, 你的螢幕它看得到, 鍵盤它也能打.

> 一個讓 AI 真正在你的電腦上工作的工具

---

#### 動手做: Bookmark 三個供應商的 Chatbot

[ChatGPT](https://chatgpt.com/), [Claude](https://claude.ai/), [Gemini](https://gemini.google.com/app)

#### 動手做: 安裝 Claude Code

[Claude Code DOC Quick Start](https://code.claude.com/docs/zh-TW/quickstart)

Mac 找不到 Claude 的路徑

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
```

---

### 2-2 Git

#### 動手做: 安裝 Git

```bash
git --version
```

有輸出版本號（例如 `git version 2.x.x`）即代表安裝成功.

#### 動手做: 告訴 Git 你是誰, 這個設定只需要做一次.

```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "your.email@example.com"
```

---

#### Git 和 GitHub 不是同一件事

| | Git | GitHub |
|---|---|---|
| 是什麼 | 版本控制工具 | 雲端存放平台 |
| 在哪裡 | 安裝在你的電腦 | 網站 github.com（微軟旗下）|
| 做什麼 | 在本機記錄每次變更 | 把記錄備份到雲端、分享給他人 |

---

#### Repository

簡稱 repo, 是一個有完整歷史記錄的資料夾.

#### Commit

把當前的變更打包成一個有名字的歷史節點, 附上說明記錄「這次改了什麼、為什麼改」.

#### Remote

本機的 repo 只活在你的電腦裡. 遠端 repo 是在 GitHub 建立一份備份.

```
你的電腦（本機 repo）
    ^
    |  pull: 把雲端的最新變更拉回本機
    |  push: 把本機的新 commit 上傳到雲端
    v
遠端 repo（GitHub / GitLab）
    |  pull  ^  push
    v        | 
同事的電腦（本機 repo）
```

---

### 2-3 VS Code

#### 動手做: 安裝和基本操作

開啟資料夾, 建立新檔案

| 訂閱 | Windows | Mac  |
|:-|:-|:-|
| Claude Pro| `C:\Users\<名稱>\.claude\CLAUDE.md` | `~/.claude/CLAUDE.md` |
| ChatGPT Plus| `C:\Users\<名稱>\.codex\AGENT.md` | `~/.codex/AGENT.md` |
| Gemini Advanced | `C:\Users\<名稱>\.gemini\GEMINI.md` | `~/.gemini/GEMINI.md` |

#### Markdown 和 AI 說同一種語言

如果你的工作筆記本來就是 Markdown, 就等於你和 AI 之間不需要格式翻譯. 提示詞、輸出、儲存, 都在同一個格式生態裡流轉.

---

```
# 全域偏好設定

- 在未指定專案目錄的一般對話中 (例如當前工作目錄不屬於任何特定專案) , 除非使用者明確要求, 否則只以模型知識為基礎協作, 不主動探索或讀取當前工作目錄以外的任何檔案或專案.
- 不主動觸發任何 custom skill.即使當下對話情境符合某個 skill 的描述, 不自行判斷並調用.Skill 的使用, 必須由使用者明確以 slash command 發起.

## Markdown 生成慣例

- 預設不使用粗體　`**text**`. 若需強調, 優先改用標題層級, 條列結構或程式碼區塊來呈現層次, 而非加粗文字.
- 預設不使用 emoji.除非使用者明確要求, 否則所有回應與檔案內容均不得包含表情符號.
- 預設不使用破折號　`－－` 或  `－` 或 `--` 或 `-`, 也不使用頓號 `、`, 若需連接, 轉折或補充說明, 優先改用逗號, 句號分句.
- 其他限制標點符號使用半形規範:
  - 逗號 ,
  - 句號 .
  - 分號 ;
  - 冒號 :
  - 斜線 /
  - 反斜線 \
  - 引號 ""
  - 括號 ()
  - 問號 ?
  - 驚嘆號 !
- 半形標點, 後方加一個半形空格, 避免視覺擠在一起.
```

---

#### 動手做: 拿到一份你自己的副本

| | Fork | Clone |
|---|------|-------|
| 動作發生在 | GitHub 網站 | 你的電腦 |
| 做的事 | 把別人的 repo 複製一份到你自己的帳號 | 把一份 repo（自己的或別人的）下載到本機 |
| 結果 | 你的帳號下多了一份完全獨立的 repo | 本機資料夾裡有一份可以編輯的副本 |

1. VS code 建立新資料夾
2. 開啟 [一天一AI — 文章摘要索引](https://github.com/AlleninTaipei/one_day_one_ai), 點擊右上角的 Fork
3. Fork 完成後, 網址會變成 `github.com/你的帳號/one_day_one_ai`, 這是你自己的副本
4. 點擊綠色的 Code 按鈕, 複製 HTTPS 網址, 在終端機執行:

```bash
git clone https://github.com/你的帳號/one_day_one_ai.git
```

---

#### 動手做: 完整工具鏈閉環

VS code 開啟資料夾 → AI 生成 → VS Code 編輯 → GitHub New Repo → Git 版控 → GitHub 雲端備份

Windows VS Code 終端機打不開 Claude Code

powershell 指令

```bash
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

---

## 小結: Part 2 概念關係總覽

| 主題 | 是什麼 | 關鍵認識 |
|------|-------|---------|
| Claude Code | 在你電腦裡工作的 AI Agent | 從給建議的電話顧問, 到能看螢幕、能動鍵盤的同事 |
| Git | 版本控制（Repo / Commit / Remote）| 版本記錄讓每一次操作都可以回溯, push 讓工作不綁在單一台電腦上 |
| GitHub | 雲端存放平台 | 備份、跨裝置存取, Fork 把別人的 repo 複製成自己的副本, Clone 下載到本機 |
| VS Code / Markdown | 工作環境與文件格式 | CLAUDE.md 是給 AI 的全域指令, Markdown 讓人與 AI 共讀同一種格式 |

---

> 恭喜你. 你已經理解新的工作方式. 你安裝了工具、下了指令、把成果推上了 GitHub.
> 從這一刻起, AI 不再只是你聽說過的東西, 而是坐在你旁邊、等你開口的同事.
