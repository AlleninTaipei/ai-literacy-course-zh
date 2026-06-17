# Claude Code 執行 Git 操作的前提條件

Claude Code 本身不需要特殊設定就能執行 git 指令，關鍵在於你的 macOS 環境本身是否已正確設定。

---

## 必要條件

### 1. Git 已安裝

```bash
git --version
```

macOS 通常內建，或透過 Xcode Command Line Tools 安裝：

```bash
xcode-select --install
```

### 2. Git 全域身份設定（commit 必須）

```bash
git config --global user.name "你的名字"
git config --global user.email "你的 Email"
```

> 沒有這個，`git commit` 會失敗。

### 3. 遠端倉庫的認證（push 必須）

這是最常見的卡點。GitHub 已停止使用密碼，需用以下其中一種方式：

- **SSH Key（推薦）**：產生 SSH key 並加到 GitHub 帳號

  ```bash
  ssh-keygen -t ed25519 -C "你的Email"
  # 然後把 ~/.ssh/id_ed25519.pub 的內容貼到 GitHub Settings > SSH Keys
  ```

- **Personal Access Token (PAT)**：在 GitHub 產生 token，push 時當密碼使用（配合 macOS Keychain 儲存）

---

## 關於 Claude Code 的權限

Claude Code 執行 git 指令時，會先詢問你是否允許（除非你在設定中開啟自動允許）。這是設計上的安全機制，特別是對於 `push`、`reset --hard` 等不可逆操作。

---

## 快速確認你的環境

```bash
git config --global user.name    # 應顯示你的名字
git config --global user.email   # 應顯示你的 Email
ssh -T git@github.com            # 應顯示 "Hi username! You've successfully authenticated"
```
