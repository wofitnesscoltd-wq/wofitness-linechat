# 專案須知（給 Claude）

## 「上線 / 部署」的定義 — 一律指「更新到正式版」（重要）
- **正式版**＝使用者手機上開的 app，由 **Cloudflare Workers 部署 `main` 分支**
  （worker 名稱 `mia-tia-3c`；靜態檔在 `./public`，Worker 入口 `src/index.ts` 以
  `env.ASSETS` 提供 `./public`）。
- **功能分支（`claude/*`）的 Cloudflare 部署只是「預覽」，不是正式版。**
  把變更推到功能分支、PR 顯示「Deployment successful」≠ 使用者看得到。
- 因此本專案「上線 / 已部署 / 更新到正式版」**一律指：把功能分支的 PR 合併進
  `main`**，讓 Cloudflare 重新部署正式版。
- **工作流程**：在指定功能分支開發 → 推送 → 開 PR → **預設把 PR 合併進 `main`
  發佈到正式版**（變更有風險或不明確時，先用 AskUserQuestion 跟使用者確認再合併）。
- **回報用語**：只有在 `main` 已更新、Cloudflare 會重新部署正式版時，才說
  「已上線 / 已更新到正式版」；若只推到功能分支，要明講「還在預覽、尚未上正式版」。
- **驗證上線**：版本字串在 `public/3c.html`（`var APP_VER = "v2.x · …"`），顯示在
  app 頁尾與睡眠頁橫幅。發佈後請使用者重整頁面、確認版本號有變。

## 其他
- `public/index.html` 是無關的 Cloudflare 範本；**真正的 app 是 `public/3c.html`**
  （單一檔案，內含全部 HTML / CSS / JS）。
