# FlClash AUR Auto-Updater

自動維護 [flclash-appimage-bin](https://aur.archlinux.org/packages/flclash-appimage-bin) AUR 套件。

## 運作方式

GitHub Actions 每天 UTC 00:00 (台灣時間 08:00) 自動執行：

1. 檢查 [FlClash](https://github.com/chen08209/FlClash) 最新版本
2. 與目前 AUR 版本比對
3. 如果有新版本：
   - 更新 PKGBUILD 的 `pkgver` 和 `sha256sum`
   - 產生新的 `.SRCINFO`
   - 推送到 AUR

## 設定步驟

### 1. 建立 GitHub Repo

```bash
gh repo create flclash-aur-autoupdate --public --source=. --push
```

### 2. 產生專用 SSH 金鑰

```bash
ssh-keygen -t ed25519 -f ~/.ssh/aur_deploy -N "" -C "github-actions-aur"
```

### 3. 將公鑰加到 AUR

複製公鑰內容並加到 AUR 帳號設定：
```bash
cat ~/.ssh/aur_deploy.pub
```

### 4. 將私鑰加到 GitHub Secrets

```bash
cat ~/.ssh/aur_deploy
```

到 GitHub repo → Settings → Secrets and variables → Actions → New repository secret
- Name: `AUR_SSH_KEY`
- Value: 貼上私鑰內容

## 手動觸發更新

GitHub repo → Actions → Update AUR Package → Run workflow

## 授權

GPL-3.0
