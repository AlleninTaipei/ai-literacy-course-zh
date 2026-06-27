# Marp

## 用文字撰寫簡報, 給上班族的 Marp 入門指南

## 前言

Marp 是一套讓使用者用 Markdown 純文字撰寫簡報的工具生態系. 上班族常常需要快速產出會議簡報, 教育訓練教材或專案報告, 透過 Marp 可以省去在 PowerPoint 中反覆調整版面的時間, 專注在內容本身, 並能用 Git 等版本控制工具追蹤簡報的修改歷史.

本文件將介紹 Marp 的基本概念, 語法規則, 以及辦公場景中的實際應用方式.

## 什麼是 Marp

Marp 全名是 Markdown Presentation Ecosystem, 由 Marp Team 開發與維護. 它讓使用者用一份 Markdown 檔案描述整份簡報, 再透過工具渲染成可投影或可分享的格式. 主要組成包括:

- Marp Core, 負責把 Markdown 轉換成簡報用的 HTML 與 CSS
- Marp CLI, 命令列工具, 可將 Markdown 輸出成 HTML, PDF, PPTX, PNG 等格式
- Marp for VS Code, VS Code 擴充套件, 提供即時預覽與匯出功能
- Marp Web, 線上編輯器, 不需安裝即可在瀏覽器中使用

## 安裝與啟用方式

### 方式一, VS Code 擴充套件

1. 在 VS Code 的擴充套件市集搜尋 "Marp for VS Code" 並安裝.
2. 建立一個 `.md` 檔案, 在檔案最上方加入 `marp: true`, 啟用 Marp 渲染模式.
3. 安裝完成後, 編輯器右上角會出現簡報預覽圖示, 點擊即可即時預覽投影片.
4. 透過命令面板執行 "Marp: Export Slide Deck", 可直接匯出 PDF, PPTX, PNG, HTML.

### 方式二, Marp CLI

```
npm install -g @marp-team/marp-cli
marp slide.md -o slide.pdf
marp slide.md -o slide.html
marp slide.md -o slide.pptx
```

### 方式三, Marp Web

直接在瀏覽器開啟 Marp Web 線上編輯器, 貼上 Markdown 內容即可預覽與匯出, 適合不方便安裝軟體的場合.

## 基本架構, 投影片分隔

一份 Marp 簡報由一個 Markdown 檔案組成, 檔案最上方需要一段 YAML 格式的設定區塊(稱為 front matter), 接著用 `---` 分隔每一張投影片.

```
---
marp: true
theme: default
paginate: true
---

# 第一張投影片

這裡是第一張投影片的內容.

---

# 第二張投影片

這裡是第二張投影片的內容.
```

注意, `---` 上下都需要保留空白行, 否則可能無法被正確判斷為投影片分隔線.

## 全域指令, Front Matter

寫在檔案最上方第一個 `---` 區塊內的設定, 稱為全域指令, 會套用到整份簡報. 常用的全域指令如下.

| 指令 | 說明 |
| --- | --- |
| `marp: true` | 啟用 Marp 渲染模式, 為必填項目 |
| `theme: default` | 設定主題, 可填入 default, gaia, uncover, 或自訂主題名稱 |
| `paginate: true` | 在每張投影片右下角顯示頁碼 |
| `size: 4:3` | 設定投影片比例, 可填 4:3 或 16:9 |
| `backgroundColor: #ffffff` | 設定整份簡報的背景色 |
| `color: #333333` | 設定整份簡報的文字顏色 |
| `header: 文字` | 設定每張投影片共用的頁首文字 |
| `footer: 文字` | 設定每張投影片共用的頁尾文字 |

## 區域指令, 單張投影片設定

在某一張投影片內用 HTML 註解寫指令, 可以針對單張投影片做客製化設定. 不加底線前綴的指令會從這張投影片開始, 一直套用到後面的投影片, 加上底線前綴(例如 `_color`)則只套用在當前這一張投影片.

```
---

# 一般投影片

---

<!-- _backgroundColor: black -->
<!-- _color: white -->

# 這張投影片是黑底白字, 只影響這一張

---

# 這張投影片恢復原本的設定
```

## 背景圖片與版面切版

使用 `![bg]` 語法可以把圖片設為投影片背景, 並透過關鍵字調整呈現方式.

```
![bg](image.jpg)
![bg fit](image.jpg)
![bg cover](image.jpg)
![bg left](image.jpg)
![bg right:40%](image.jpg)
```

`left` 與 `right` 可以把投影片分成左右兩欄, 一欄放圖片, 另一欄放文字內容, 適合製作對照式或說明式的版面.

## 圖片縮放

一般圖片可以用 `width` 與 `height` 關鍵字調整大小, 不需要另外撰寫 CSS.

```
![width:300px](photo.png)
![w:300 h:200](photo.png)
```

## 主題 Theme

Marp Core 內建三種主題, 分別是 default, gaia, uncover, 可在 front matter 用 `theme` 指令指定. 若公司有固定的視覺識別規範, 也可以撰寫自訂 CSS 主題, 並在 CSS 檔案開頭用 `@theme` 註解命名, 再透過 `theme` 指令套用.

部分主題額外提供 `class` 指令做版面變化, 例如 gaia 主題的 `class: invert` 可以快速切換成深色背景版面.

```
---
marp: true
theme: gaia
class: invert
---
```

## 程式碼與數學公式

Marp 支援一般的 Markdown 程式碼語法, 包含行內程式碼與區塊程式碼, 並內建語法高亮.

```
這是行內程式碼: `console.log("hi")`

\`\`\`javascript
function hello() {
  console.log("Hello, Marp")
}
\`\`\`
```

數學公式則支援 KaTeX 語法, 行內公式用單個 `$` 包住, 區塊公式用兩個 `$$` 包住.

```
行內公式: $E = mc^2$

區塊公式:
$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$
```

## 簡報備忘稿

任何不符合指令格式的 HTML 註解, 會被當作演講者備忘稿, 只有在簡報者模式下才會顯示, 不會出現在正式投影片畫面上.

```
<!-- 這段文字是演講者的提詞, 觀眾不會看到 -->
```

## 匯出格式

| 格式 | 適合用途 |
| --- | --- |
| HTML | 互動式網頁簡報, 可用瀏覽器開啟並用鍵盤或滑鼠翻頁 |
| PDF | 適合列印, 存檔, 或透過信件寄送 |
| PPTX | 匯出後可在 PowerPoint 中繼續微調 |
| PNG, JPEG | 單張投影片圖片, 適合社群媒體或即時通訊分享 |

## 上班族常見應用情境

### 內部會議簡報

```
---
marp: true
theme: default
paginate: true
header: "2026-06-21 部門週會"
---

# 本週重點摘要

- 業績達成率
- 客戶回饋整理
- 下週行動計畫
```

### 教育訓練教材

利用 `---` 把整套課程拆成多張投影片, 搭配程式碼區塊, 表格與圖片, 快速完成講義與簡報合一的教材, 同時用 Git 保留每次修訂的版本紀錄.

### 制式報告模板

先撰寫一份固定版型的 Markdown 模板, 之後每次只需要替換內容文字, 不需要重新調整版面位置, 可大幅縮短重複性報告的製作時間.

## 建議工作流程

1. 用 VS Code 撰寫 Markdown 內容, 並開啟即時預覽確認版面.
2. 用 Git 管理 `.md` 檔案, 方便追蹤每次內容修改.
3. 完成後用 Marp CLI 或 VS Code 擴充套件匯出成 PDF 或 PPTX.
4. 若需要在會議中即時呈現, 可直接使用匯出的 HTML 版本, 透過瀏覽器全螢幕播放.

## 常見錯誤提醒

1. 忘記在檔案最上方加入 `marp: true`, 導致工具沒有啟用 Marp 渲染模式.
2. 投影片分隔線 `---` 上下沒有保留空白行, 造成分頁失敗或被誤判為其他語法.
3. front matter 的 YAML 縮排寫錯, 導致指令未生效.
4. 區域指令忘記加底線前綴, 結果設定被套用到後面所有投影片, 而不是只套用在當前這一張.
5. 圖片使用本機絕對路徑, 換到其他電腦或匯出後路徑失效, 建議統一使用相對路徑.

## 快速複習表

| 語法或指令 | 用途 |
| --- | --- |
| `marp: true` | 啟用 Marp 渲染模式 |
| `---` | 分隔投影片, 或包住 front matter |
| `theme:` | 設定主題 |
| `paginate:` | 顯示頁碼 |
| `size:` | 設定投影片比例 |
| `_color:` | 只套用於當前這一張投影片的文字顏色 |
| `![bg]()` | 設定投影片背景圖片 |
| `![w:300]()` | 調整圖片寬度 |
| `class: invert` | 切換深色版面(部分主題支援) |
| `$...$` | 行內數學公式 |
| `$$...$$` | 區塊數學公式 |
| HTML 註解(無指令格式) | 演講者備忘稿 |

## 結語

Marp 把寫簡報這件事變成寫一份結構清楚的 Markdown 文件, 對於已經熟悉 Markdown 語法的上班族來說, 學習門檻非常低. 建議先從簡單的會議簡報開始練習, 熟悉投影片分隔, 全域指令與區域指令的用法後, 再進一步嘗試自訂主題與版面切版, 逐步把日常的簡報製作流程轉移到 Marp 上.
