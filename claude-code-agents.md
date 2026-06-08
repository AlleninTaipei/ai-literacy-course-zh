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

# Claude Code

## `←` for agents 用法說明

多 Agent 並行管理的控制台入口

---

### 這是什麼？

在 Claude Code 的輸入框旁，你會看到 **「← for agents」** 的提示。

按下**左方向鍵 ←**，就能開啟 **Agent View（代理視圖）**——一個集中管理所有背景 Agent session 的控制台。

兩種進入方式：

| 方式 | 操作 |
|------|------|
| 鍵盤 | 在 Claude Code 輸入框按下 `←` 左方向鍵 |
| 終端機 | 執行 `claude agents` |

---

### Agent View 能做什麼？

| 功能 | 說明 |
|------|------|
| 總覽列表 | 每列顯示各 session 的名稱、最後回應內容、上次互動時間、是否在等你輸入 |
| 等待確認 | 若某個 agent 卡住等你決定，可直接在 Agent View 內回覆，session 立即繼續執行 |
| 快速查看 | 選擇任一 session 即可預覽最後一輪對話，不需要切換視窗 |
| 切換背景 | 任何現有 session 都能用 `/bg` 指令切換成背景模式，加入 Agent View |

---

### Agent View 長什麼樣子？

```
● Session 1 — 寫測試          [完成]
  已完成 unit tests，等待 review

◎ Session 2 — 資料庫遷移      [等待確認]
  需要你確認：要刪除舊欄位嗎？

◉ Session 3 — 撰寫文件        [執行中]
  正在產生 API 文件中…
```

> 選擇「等待確認」的 session 直接回覆，agent 就會繼續跑，不需要重新啟動。

---

### 實際使用流程

1. 啟動多個平行任務，讓各個 agent 在背景各自執行
2. 按 `←` 進入 Agent View，一眼看清所有 session 狀態
3. 找到標示「等待確認」的 session，直接在 Agent View 內輸入回覆
4. 按右方向鍵 `→` 或 Enter 進入該 session 繼續深入操作

```bash
# 將目前 session 切換成背景執行，加入 Agent View
/bg

# 或直接從新終端機開啟 Agent View
claude agents

# 在 Agent View 裡，用方向鍵選 session，← 進入、→ 返回
```

[Agent view in Claude Code — Anthropic](https://claude.com/blog/agent-view-in-claude-code)
