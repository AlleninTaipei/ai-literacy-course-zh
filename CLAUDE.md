# 專案慣例

## 匯出 HTML

每份教材的 Markdown 來源會匯出成瀏覽模式 HTML, 匯出工具是 Markdown Preview Enhanced. 專案已不再支援簡報模式(Marp), 對應的 `*-slide.html` 匯出檔已全部移除.

匯出時有個已知行為: 原始 Markdown 裡指向同層其他檔案的相對連結(例如 `neural-network-demo.html`), 有時會被展開成本機絕對路徑(例如 `file:///f:\work\ai-literacy-course-zh\neural-network-demo.html`). 這種連結只在原作者的本機路徑下能打開, 推上 GitHub Pages 後會失效.

如果手動編輯或修正 HTML 時看到 `href="file:///..."` 這種連結, 應改成純檔名的相對連結(例如 `href="neural-network-demo.html"`).

## pre-commit hook

`.githooks/pre-commit` 會在每次 commit 前, 自動把首頁 `index.html` 頁尾的「最後更新」日期改成今天, 重新加入這次 commit, 不需要手動維護這個日期. 這個 hook 設計成失敗時一律放行(fail open), 不會因為腳本本身出錯而卡住任何人的 commit.

這個 hook 只在本機 repo 設定 `core.hooksPath` 之後才會生效(設定存在 `.git/config`, 不會隨 clone/fork 傳播). 對於 clone 這個 repo 來做 Git 練習的學員來說, 沒有額外動作就不會觸發這個機制, 也就不會被它影響.
