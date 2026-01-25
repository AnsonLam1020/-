# AGENTS.md - Anson Game 開發指南

## 項目概述
Anson Game 是一個基於 HTML5 的遊戲平台，包含多個小遊戲和互動遊戲。所有遊戲都使用純 HTML、CSS 和 JavaScript 開發，支援中文界面。

## 項目結構
```
/
├── index.html          # 主頁面 - 遊戲中心
├── game1.html          # 貪食蛇遊戲
├── game2.html          # 彈跳方塊遊戲
├── game3.html          # 包剪揼遊戲
├── game4.html          # 極速賽車遊戲
├── game5.html          # 密室逃脫遊戲
└── AGENTS.md           # 本文件
```

## 開發環境與工具

### 測試與驗證
- **瀏覽器測試**: 直接在瀏覽器中打開 HTML 文件進行測試
- **響應式測試**: 使用瀏覽器開發者工具測試不同螢幕尺寸
- **控制台檢查**: 使用 F12 開發者工具檢查 JavaScript 錯誤

### 驗證工具
- **HTML 驗證**: 使用 [W3C Validator](https://validator.w3.org/)
- **CSS 驗證**: 使用 [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
- **JavaScript 語法檢查**: 瀏覽器控制台

## 代碼風格指南

### HTML 結構
- **文檔類型**: 使用 `<!DOCTYPE html>`
- **語言設定**: 
  - 主頁面使用 `lang="zh-HK"`
  - 遊戲頁面使用 `lang="zh-TW"`
- **字符編碼**: 必須使用 `<meta charset="UTF-8">`
- **響應式設置**: 必須包含 `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- **語義化標籤**: 使用 `<header>`, `<main>`, `<section>`, `<footer>` 等語義化標籤

### CSS 樣式規範
- **重置樣式**: 在每個文件開頭使用 `* { margin: 0; padding: 0; box-sizing: border-box; }`
- **字體設定**: 
  - 主要字體: `'Segoe UI', 'Microsoft JhengHei', sans-serif`
  - 遊戲字體: `'Microsoft JhengHei', 'Segoe UI', sans-serif`
- **顏色主題**: 
  - 背景漸變: `linear-gradient(135deg, #1a1a2e 0%, #16213e 100%)`
  - 主色調: `#4ecdc4`, `#45b7d1`, `#ff6b6b`
  - 文字顏色: `#fff` (白色), `#a9b7c6` (灰色)
- **響應式設計**: 必須包含媒體查詢
  - 平板: `@media (max-width: 768px)`
  - 手機: `@media (max-width: 480px)`
- **動畫效果**: 使用 CSS transitions 和 animations
- **網格佈局**: 使用 CSS Grid 和 Flexbox 進行佈局

### JavaScript 編碼規範
- **嚴格模式**: 在腳本開始使用 `'use strict';`
- **變數宣告**: 使用 `const` 和 `let`，避免使用 `var`
- **函數命名**: 使用 camelCase，例如 `startGame()`, `updateScore()`
- **事件處理**: 使用 `addEventListener` 而不是 `onclick` 屬性
- **錯誤處理**: 使用 try-catch 處理可能的錯誤
- **註釋**: 為複雜邏輯添加中文註釋

### 命名約定
- **文件命名**: 使用小寫字母和連字符，例如 `game-snake.html`
- **CSS 類名**: 使用 kebab-case，例如 `.game-container`, `.play-button`
- **JavaScript 變數**: 使用 camelCase，例如 `gameScore`, `isGameRunning`
- **常量**: 使用 UPPER_SNAKE_CASE，例如 `MAX_PLAYERS`, `GAME_SPEED`

### 遊戲開發模式
- **Canvas 遊戲**: 使用 HTML5 Canvas API 進行遊戲渲染
- **狀態管理**: 使用全局變數管理遊戲狀態
- **動畫循環**: 使用 `requestAnimationFrame` 或 `setInterval`
- **本地存儲**: 使用 `localStorage` 保存高分和設置
- **響應式控制**: 同時支援鍵盤和觸控操作

## 國際化與本地化
- **語言支援**: 繁體中文 (zh-HK, zh-TW)
- **文字編碼**: UTF-8
- **數字格式**: 使用阿拉伯數字
- **日期時間**: 使用 24 小時制格式

## 性能優化
- **資源加載**: 
  - 使用 CDN 加載外部庫 (Font Awesome, MediaPipe)
  - 圖片使用 WebP 格式
- **代碼優化**: 
  - 避免全局變數污染
  - 使用事件委託
  - 適當使用防抖和節流
- **動畫性能**: 
  - 使用 CSS transforms 而不是 position
  - 避免頻繁的 DOM 操作

## 安全考慮
- **XSS 防護**: 對用戶輸入進行適當的轉義
- **CSP 設置**: 考慮添加 Content Security Policy
- **HTTPS**: 生產環境建議使用 HTTPS

## 測試指南
### 單元測試
由於是純前端項目，主要進行以下測試：
- **功能測試**: 驗證遊戲邏輯正確性
- **兼容性測試**: 測試不同瀏覽器兼容性
- **響應式測試**: 測試不同設備尺寸
- **性能測試**: 檢查動畫流暢度和內存使用

### 調試技巧
- 使用 `console.log()` 進行調試
- 使用瀏覽器開發者工具的斷點功能
- 檢查網絡請求和資源加載
- 監控內存和性能指標

## 部署說明
- **靜態托管**: 可部署到任何靜態網站托管服務
- **文件結構**: 保持相對路徑引用
- **壓縮優化**: 生產環境可壓縮 CSS 和 JavaScript
- **緩存策略**: 設置適當的緩存頭

## 維護指南
- **版本控制**: 使用 Git 進行版本管理
- **代碼審查**: 提交前進行代碼審查
- **文檔更新**: 更新功能時同步更新文檔
- **測試覆蓋**: 確保新功能有對應測試

## 常見問題解決
- **字體顯示問題**: 確保加載了中文字體
- **觸控事件**: 移動設備上需要添加觸控事件監聽
- **性能問題**: 檢查動畫循環和 DOM 操作頻率
- **兼容性**: 使用 polyfill 解決舊瀏覽器兼容性

## 開發工具推薦
- **編輯器**: VS Code, Sublime Text
- **瀏覽器**: Chrome, Firefox (帶開發者工具)
- **設計工具**: Figma, Adobe XD
- **版本控制**: Git, GitHub

## 聯繫信息
如有問題或建議，請通過以下方式聯繫：
- 項目維護者: Anson
- 最後更新: 2023年