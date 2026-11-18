# 接續說明（給 Claude Code）

> 這個檔案只在 `wall-reset` 分支上。合併到 `main` 之前要刪除它。

## 專案
- camp-party：只有一個 `index.html` 的性別揭曉網站，掛在 GitHub Pages（從 `main` 自動發布）。
- 後端：Firebase Realtime Database。安全規則在 `database.rules.json`，要在 Firebase Console 手動發布。
- 頁面模式：
  - 一般親友：沒有參數。
  - `?host=<密碼>`：主持人。
  - `?keeper=<密碼>`：保密人。
  - `?preview=boy|girl`：本機模擬，不連 Firebase。
- 主持人密碼不會寫在 repo 裡，需要時直接問使用者。

## 目前進度
- `main`：已上線，含孕期線索卡片（commit b6f9ea8）。
- `wall-reset` 分支（commit 603fc7b）：營火祝福牆的「🧹 重置」按鈕，**已寫好，但還沒測試**。
  - 只有 `?host=` 和 `?preview=` 頁面看得到（`#wallReset`，由 `initWallReset()` 顯示）。
  - 按下後確認一次，再呼叫 `api.host('clear_votes')`，刪除整個 `votes`。
  - 效果：留言和選邊站的票一起清掉，帳篷人氣歸零，大家可以重新投票。
  - 規則已允許主持人寫 `votes`，不用改規則。

## 接下來要做
1. 用 `index.html?preview=boy` 測試重置按鈕：
   - 祝福牆和帳篷人氣都歸零。
   - 投票表單重新出現。
2. 跟使用者確認行為。目前是連票一起清掉，因為每則留言和那個人的票存在同一筆資料裡。
3. 使用者同意之後：
   - 刪除這個 HANDOFF.md。
   - 合併到 `main` 並 push。
   - commit 和 push 都要等使用者說了才做。

## 注意
- 用無頭 Chrome 測試時，只能關掉自己開的那個行程，不要把所有 chrome.exe 都關掉，以免關到使用者自己的瀏覽器。
- 用 Firebase 實測時：
  - 要用 http://localhost 開網頁，用 file:// 開會連不上。
  - 測完要把測試資料清掉。
