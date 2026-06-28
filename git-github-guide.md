# Git & GitHub

## 版本控制與雲端協作, 給職場工作者的 Git & GitHub 入門指南

## 前言

無論是程式碼, 設計檔案, 還是各類文件, 只要是多人協作或需要保留修改歷史的工作, 都會遇到版本管理的問題. Git 是目前最廣泛使用的版本控制工具, GitHub 則是建立在 Git 之上的雲端平台, 兩者搭配可以讓團隊清楚追蹤每一次修改, 方便回溯, 比對與協作.

本文件將先說明 Git 與 GitHub 各自的角色與差異, 再介紹常用指令與操作流程, 最後提供辦公場景中的實際應用範例.

## 什麼是 Git

Git 是由 Linus Torvalds 於 2005 年開發的分散式版本控制系統. 它的核心概念是把專案內容的每一次變更記錄成一個快照(commit), 並讓使用者可以在不同的時間點之間切換, 比對, 或合併. Git 主要在本機運作, 不需要連網也能查看歷史紀錄與切換版本.

## 什麼是 GitHub

GitHub 是一個基於 Git 的雲端代管平台, 讓使用者可以把本機的 Git 專案(稱為 repository, 簡稱 repo)存放到雲端, 並提供以下額外功能:

- Pull Request, 讓團隊成員審查彼此的修改內容後再合併
- Issue, 用來追蹤待辦事項, 錯誤回報或需求討論
- Actions, 自動化流程工具, 可用於測試, 建置或部署
- Projects, 看板式的專案管理工具
- Wiki 與 README, 用於存放專案說明文件

## Git 與 GitHub 的關係

Git 是版本控制的核心技術, GitHub 是其中一個提供 Git 代管服務的雲端平台, 兩者並非同一件事. 除了 GitHub 之外, 市場上還有 GitLab, Bitbucket 等類似服務, 都是建立在 Git 之上, 提供類似的雲端協作功能. 換句話說, 即使完全不使用 GitHub, 仍然可以單獨使用 Git 在本機進行版本控制, 只是少了雲端備份與多人協作介面.

## 安裝與初始設定

安裝完成後, 建議先設定使用者名稱與信箱, 這些資訊會記錄在每一次的 commit 中.

```
git config --global user.name "你的名字"
git config --global user.email "you@example.com"
```

## 基本概念

| 名詞 | 說明 |
| --- | --- |
| Repository(repo) | 一個被 Git 追蹤管理的專案資料夾 |
| Working Directory | 目前在電腦上看到, 正在編輯的檔案內容 |
| Staging Area | 準備要納入下一次 commit 的暫存區 |
| Commit | 一次內容快照, 記錄當下所有被加入暫存區的變更 |
| Branch | 一條獨立的開發線, 方便同時進行多項修改而不互相干擾 |
| HEAD | 目前所在的分支或版本位置 |
| Remote | 遠端的版本庫位置, 例如 GitHub 上的 repo |

## 建立與複製專案

```
git init
git clone https://github.com/帳號/專案名稱.git
```

`git init` 用於在現有資料夾中建立新的 Git 專案, `git clone` 用於把遠端已存在的 repo 完整複製到本機.

## 常用指令一覽

```
git status            查看目前哪些檔案有變更
git add 檔案名稱        把指定檔案加入暫存區
git add .              把所有變更加入暫存區
git commit -m "訊息"    建立一次commit, 並寫明變更內容
git log                查看commit歷史紀錄
git diff               查看尚未加入暫存區的內容差異
```

## 與遠端同步

```
git remote add origin https://github.com/帳號/專案名稱.git
git push origin main
git pull origin main
git fetch origin
```

`push` 是把本機的 commit 上傳到遠端, `pull` 是把遠端的最新內容下載並合併到本機, `fetch` 則只下載遠端資訊, 不會自動合併.

## 分支與合併

```
git branch                建立並查看分支列表
git branch 新分支名稱       建立新分支
git switch 分支名稱         切換到指定分支
git merge 分支名稱          把指定分支合併進目前所在的分支
```

當兩個分支修改了同一個檔案的同一個位置, 合併時會出現衝突(conflict), Git 會在檔案中標記出衝突區塊, 需要手動決定保留哪一部分內容, 再重新 commit 完成合併.

## GitHub 基本操作流程

1. 在 GitHub 網站建立一個新的 repository.
2. 在本機用 `git clone` 把這個 repository 複製下來, 或用 `git remote add` 把現有的本機專案連結到這個 repository.
3. 在本機建立分支, 進行修改, 並完成 commit.
4. 用 `git push` 把分支上傳到 GitHub.
5. 在 GitHub 上開啟 Pull Request, 讓其他成員審查後再合併進主分支.

## GitHub CLI, 給熟悉終端機的使用者

GitHub 也提供官方的指令列工具, 稱為 GitHub CLI(指令為 `gh`), 讓使用者不需要切換到瀏覽器, 直接在終端機中建立 Pull Request, 管理 Issue, 或查看審查狀態. 這也是 Claude Code 在處理 GitHub 相關任務時所使用的方式, 也就是說, 當你請 Claude Code 協助開啟一個 Pull Request 或建立一個 Issue 時, 它背後實際執行的就是這一類指令.

### 登入設定

```
gh auth login
```

依照畫面提示選擇登入方式(瀏覽器或權杖), 完成後即可用 `gh` 指令操作有權限的 repository, 不需要額外設定 SSH 金鑰或權杖.

### 常用指令

```
gh repo clone 帳號/專案名稱     複製遠端repo到本機
gh pr create                 建立一個Pull Request
gh pr list                    查看目前open的Pull Request列表
gh pr view 編號 --web          在瀏覽器中開啟指定的Pull Request
gh pr checkout 編號            把指定的Pull Request切換到本機分支
gh issue create                建立一個Issue
gh issue list                  查看目前open的Issue列表
```

### 與前面流程的對照

前面 "GitHub 基本操作流程" 一節介紹的是在網頁上建立 Pull Request 的方式, 改用 `gh pr create` 則可以在完成 `git push` 後, 不離開終端機就直接建立同一個 Pull Request. 對於習慣在終端機或 VS Code 內建終端機工作的使用者, 可以減少在瀏覽器與編輯器之間來回切換的次數.

## 認證方式, HTTPS 與 SSH

GitHub 提供兩種主要的連線認證方式. HTTPS 方式需要搭配個人存取權杖(Personal Access Token)登入, SSH 方式則需要先在本機產生金鑰, 並把公開金鑰新增到 GitHub 帳號設定中, 之後連線就不需要每次輸入密碼.

```
ssh-keygen -t ed25519 -C "you@example.com"
```

## .gitignore

`.gitignore` 是一個純文字檔案, 用來列出不希望被 Git 追蹤的檔案或資料夾, 常見項目包括暫存檔, 編譯產出檔, 或包含密碼與金鑰等敏感資訊的設定檔.

```
node_modules/
.env
*.log
```

## 職場工作者常見應用情境

### 多人協作的文件版本控制

把報告, 規格書, 或前面提到的會議記錄 Markdown 檔案放進 Git repo 管理, 每次修改都透過 commit 留下紀錄, 團隊成員可以清楚知道是誰在什麼時候做了什麼修改, 也能隨時回溯到之前的版本.

### 程式碼審查與協作

開發人員透過分支進行開發, 再以 Pull Request 的方式提交修改, 讓其他成員在合併前先進行審查, 確保程式碼品質與一致性.

### 知識庫與專案文件集中管理

把專案的 README, SOP, 操作手冊都存放在同一個 GitHub repository 中, 搭配 Wiki 或 Markdown 檔案, 方便團隊成員查閱, 也能透過 commit 歷史了解文件演進過程.

## 常見錯誤提醒

1. commit 訊息寫得不清楚, 例如只寫 "更新", 之後難以從歷史紀錄判斷修改內容.
2. 直接在 main 或 master 分支上進行修改, 沒有先建立獨立分支, 增加團隊協作風險.
3. 使用 `git push --force` 強制推送, 可能覆蓋掉其他人已上傳的內容, 使用前務必確認影響範圍.
4. 把含有密碼或金鑰的設定檔誤加入 commit, 上傳到遠端後即使刪除, 歷史紀錄中仍可能留有痕跡.
5. 遇到合併衝突時直接放棄修改或任意刪除衝突標記, 沒有仔細確認保留的內容是否正確.

## 快速複習表

| 指令 | 用途 |
| --- | --- |
| `git init` | 建立新的 Git 專案 |
| `git clone` | 複製遠端 repo 到本機 |
| `git status` | 查看目前變更狀態 |
| `git add` | 把變更加入暫存區 |
| `git commit -m` | 建立一次commit |
| `git push` | 把本機commit上傳到遠端 |
| `git pull` | 下載並合併遠端最新內容 |
| `git branch` | 查看或建立分支 |
| `git switch` | 切換分支 |
| `git merge` | 合併指定分支 |
| `git log` | 查看commit歷史 |
| `.gitignore` | 設定不被追蹤的檔案清單 |
| `gh auth login` | 登入 GitHub CLI |
| `gh pr create` | 在終端機中建立 Pull Request |
| `gh issue create` | 在終端機中建立 Issue |

## 結語

Git 提供版本控制的核心能力, GitHub 則在這個基礎上加上雲端備份與團隊協作功能, 兩者搭配學習可以同時掌握本機操作與遠端協作的完整流程. 建議先從個人專案練習 commit 與分支操作開始, 熟悉之後再嘗試與團隊成員一起使用 Pull Request 進行協作, 逐步把日常的文件與專案管理工作都納入版本控制.
