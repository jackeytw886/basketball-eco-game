# File Map — P016 檔案地圖

核對基準：`64f0256d809b1a99a8ef04c071d9038614e1e263`。下表列出整理前檔案，大小來自 Git tree；新增管理文件另列於文末。

| 路徑 | 大小（bytes） | 類型 |
| --- | ---: | --- |
| [README.md](../README.md) | 70 | md |
| [index.html](../index.html) | 35486 | html |

## 管理入口

README.md、AGENTS.md、HANDOFF.md、PROJECT.json、CLAUDE.md、GEMINI.md、.github/copilot-instructions.md、docs/VERIFICATION.md。

## 檔內結構（行號索引，2026-10-18 Claude 依基準 `f36a556` 整理）

只讀需要的段落；標 ⚠️ 的是超長單行資料，不要整行載入。

| 約略行號 | 內容 |
| ---: | --- |
| 7–352 | `<style>` |
| 354–430 | HTML 介面 |
| 431–1177 | 主程式 `<script>` |
| 435–474 | 設定 `TOTAL_TIME`、`BINS`（4 桶）、`ITEMS`（12 題） |
| 482–785 | 8×8 LED 圖案：色碼 `CLR`、圖樣 `LED` |
| 786–867 | LED 繪製 `drawMatrix()`、音效 `SFX` |
| 868–934 | 粒子、得分飄字、遊戲狀態變數、`binAnim` |
| 935–1004 | 回收桶建立、`startGame()`、計時、`nextItem()` |
| 1005–1100 | `handleClick()`、`onCorrect()`、`onWrong()`、`gameOver()`、`showLevelUp()` |
| 1101–1177 | HUD 更新、LED 動畫迴圈、鍵盤 1～4（第 1164 行）、初始化 |
