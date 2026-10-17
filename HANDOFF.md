# Handoff — P016 環保投籃・第一版（垃圾分類大挑戰）

- 更新時間：2026-10-18T03:25+08:00
- 更新者：Claude（逐檔讀原始碼，撰寫專案交接）
- 倉庫：https://github.com/jackeytw886/basketball-eco-game
- 分支：main
- 本次基準 SHA：`f36a55670f71bb6d159406cc32b6a7af8fa3bc06`（Codex 管理整理提交）
- 核對層級：已讀全部原始碼；已執行語法檢查與無頭瀏覽器冒煙測試（見 docs/VERIFICATION.md）；**未接實體投籃機**。

## 1. 這是什麼

環保投籃機的**第一版網頁模擬**：畫面中央出現一個垃圾（球），玩家點四個回收桶之一（或按鍵盤 1～4）把它投進去，60 秒內看能分對幾個。每個回收桶上方有一塊 **8×8 LED 矩陣**動畫，模擬實體投籃機籃框上的燈板。

- 線上網址：https://jackeytw886.github.io/basketball-eco-game/ （GitHub Pages）
- 後續版本：**P004**（basketball-eco-gamev2，2D 8×8 版＋3D 模擬＋攝影機投籃）。兩者分類方式不同（本版：紙類／塑膠／玻璃／廚餘；P004：資源回收／廚餘／一般垃圾／有害垃圾），是各自獨立的程式，不是同一份檔案的版本。

## 2. 檔案

只有 `index.html`（約 35 KB、1,180 行）；外部依賴只有 Google Fonts，可離線。行號索引見 docs/FILE-MAP.md。

## 3. 程式怎麼運作

| 部分 | 位置／名稱 | 說明 |
| --- | --- | --- |
| 設定 | `TOTAL_TIME = 60` | 限時 |
| 回收桶 | `BINS` | `paper` 紙類（鍵 1）、`plastic` 塑膠（2）、`glass` 玻璃（3）、`organic` 廚餘（4），各有顏色、圖示、舉例 |
| 題庫 | `ITEMS`（12 題） | 報紙、紙箱、紙杯、寶特瓶、塑膠袋、吸管、玻璃瓶、玻璃罐、果皮、菜渣、蛋殼、剩飯；每題附一則環保小知識 `fact` |
| LED 圖案 | `CLR`（色碼）、`LED`（8×8 圖樣）、`drawMatrix(el, pattern)` | 每桶待機圖示、答對打勾、答錯叉叉、慶祝星星、升級彩虹、待機籃球彈跳；圖樣用字元字串 `P('bBBBBBBb', …)` 表示 |
| 動畫狀態 | `binAnim[binId] = { frame, mode }` | `idle`／`correct`／`wrong`／`celebrate` |
| 流程 | `startGame()` → `nextItem()` → `handleClick(binId)` → `onCorrect()`／`onWrong()` → `gameOver()` | 投出後 380 ms 判定；答對 1.5 秒、答錯 1.8 秒後出下一題 |
| 計分 | `onCorrect()` | 每題 10 分 × 連擊倍率（最多 5 倍）；每答對 5 題升一級（`showLevelUp()`） |
| 結算 | `gameOver()` | ≥300 分「環保達人」、≥150「分類高手」、其他「繼續加油」 |
| 音效 | `SFX`（Web Audio 合成）、`toggleSound()` | 投球、答對、連擊、答錯、倒數、升級、結束 |
| 特效 | `spawnParticles()`、`showScorePopup()` | 粒子與得分飄字 |

## 4. 與實體裝置的關係

LED 圖樣就是設計給實體 8×8 燈板（WS2812 一類）的動畫，但本倉庫**沒有** Arduino 程式、沒有 WebSerial，也沒有記錄實體走線方向；要上實機需要把 `LED` 圖樣轉成韌體資料並核對燈號順序。

## 5. 已知問題與待辦

- 計分沒有存檔（重新整理就歸零），也沒有排行榜。
- 題庫只有 12 題、玻璃類只有 2 題；分類以本版四類為準，與 P004 的四類不同，整併前要先決定採用哪一套分類。
- 「升級」只影響畫面效果，不會加快速度或改變題目難度。

## 6. 測試方式

直接開 `index.html`。自動化測試可呼叫 `startGame()`、`handleClick('paper')`，或送出鍵盤 `1`～`4`；狀態在全域變數 `state`、`score`、`timeLeft`、`streak`、`level`、`currentItem`。

## 7. 版本沿革

- 2026-02-22：經 EZPage 部署。
- 2026-10-17：Codex 管理整理（代號 P016、AI 入口文件）。
- 2026-10-18：Claude 補寫本交接。

## 版本定位

基準 SHA 定位本次文件修改前的程式；本次文件提交由此檔所在的 Git 提交與倉庫歷史定位，不預填同一提交自己的 SHA。
