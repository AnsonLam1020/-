# Anson Game Center - index.html 實施計劃

## 項目概述
創建一個統一的遊戲中心入口頁面 (index.html)，整合所有 5 個遊戲並提供深色/淺色主題切換功能。

## 需求分析
1. **主題要求**: 包含明亮/黑暗模式，統一設計
2. **設計風格**: 使用現有設計模式，精緻設計
3. **遊戲連結**: 連結到所有 5 個遊戲檔案 (game1.html 到 game5.html)
4. **響應式設計**: 支援移動設備
5. **功能**: 主題切換、遊戲分類、搜尋功能

## 技術架構

### 檔案結構
```
/
├── index.html              # 主入口頁面
├── shared.css             # 共享樣式 (已存在)
├── theme-toggle.js        # 主題切換功能
├── game1.html            # 貪食蛇遊戲
├── game2.html            # 彈跳方塊遊戲
├── game3.html            # 包剪揼遊戲
├── game4.html            # 極速賽車遊戲
├── game5.html            # 密室逃脫遊戲
└── plans/                # 計劃文件
```

### 設計系統
- **顏色主題**: 從現有主題檔案提取統一顏色變數
- **字體**: Space Grotesk + Noto Sans TC (繁體中文支援)
- **圖標**: Google Material Symbols
- **佈局**: CSS Grid + Flexbox 響應式設計

## 頁面結構

### 1. HTML 結構
```html
<!DOCTYPE html>
<html lang="zh-HK" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Anson Game Center - 遊戲中心</title>
    <!-- 字體和圖標 -->
    <!-- Tailwind CSS (可選) -->
    <!-- 自定義 CSS -->
</head>
<body>
    <!-- 主題切換按鈕 -->
    <!-- 頁首導航 -->
    <!-- 特色遊戲區 -->
    <!-- 遊戲分類標籤 -->
    <!-- 遊戲網格 (5個遊戲) -->
    <!-- 頁尾 -->
    <!-- JavaScript -->
</body>
</html>
```

### 2. 遊戲卡片設計
每個遊戲卡片包含：
- 遊戲圖標 (Emoji 或自定義圖形)
- 遊戲標題 (中文名稱)
- 遊戲描述 (簡短說明)
- 遊戲標籤 (類型: 經典、競速、益智等)
- 開始遊戲按鈕

### 3. 主題系統
- **深色模式**: 使用現有深色主題的顏色變數
- **淺色模式**: 使用現有淺色主題的顏色變數
- **切換機制**: 通過 JavaScript 切換 `data-theme` 屬性

## 遊戲對應表

| 遊戲檔案 | 遊戲名稱 | 類型 | 圖標 | 描述 |
|---------|---------|------|------|------|
| game1.html | 貪食蛇 | 經典 | 🐍 | 控制蛇吃掉蘋果，小心不要撞到牆壁 |
| game2.html | 彈跳方塊 | 街機 | 🧱 | 控制方塊彈跳，收集星星，避開障礙物 |
| game3.html | 包剪揼 | 互動 | ✋ | 使用手勢識別玩包剪揼遊戲 |
| game4.html | 極速賽車 | 競速 | 🏎️ | 挑戰速度極限，成為賽道王者 |
| game5.html | 密室逃脫 | 益智 | 🔐 | 解開謎題，逃離密室 |

## 功能模塊

### 1. 主題切換模塊
```javascript
// theme-toggle.js
function toggleTheme() {
    const html = document.documentElement;
    const currentTheme = html.getAttribute('data-theme') || 'dark';
    const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
    html.setAttribute('data-theme', newTheme);
    localStorage.setItem('theme', newTheme);
}
```

### 2. 遊戲卡片組件
```html
<div class="game-card" data-game="snake">
    <div class="game-icon">🐍</div>
    <h3 class="game-title">貪食蛇</h3>
    <p class="game-description">控制蛇吃掉蘋果，小心不要撞到牆壁</p>
    <div class="game-tags">
        <span class="game-tag">經典</span>
        <span class="game-tag">街機</span>
    </div>
    <a href="game1.html" class="play-btn">開始遊戲</a>
</div>
```

### 3. 響應式設計
- **桌面版**: 5列網格佈局
- **平板版**: 3列網格佈局
- **手機版**: 1列網格佈局

## CSS 變數系統

### 深色模式變數
```css
:root[data-theme="dark"] {
    --bg-primary: #1a1a2e;
    --bg-secondary: #16213e;
    --text-primary: #ffffff;
    --text-secondary: #a9b7c6;
    --accent-primary: #4ecdc4;
    --accent-secondary: #ff6b6b;
}
```

### 淺色模式變數
```css
:root[data-theme="light"] {
    --bg-primary: #f0f8ff;
    --bg-secondary: #e6f7ff;
    --text-primary: #333333;
    --text-secondary: #666666;
    --accent-primary: #ffa500;
    --accent-secondary: #4CAF50;
}
```

## 實施步驟

1. **創建基礎 HTML 結構**
   - 設置文檔結構
   - 添加必要的 meta 標籤
   - 引入字體和圖標

2. **實現主題系統**
   - 定義 CSS 變數
   - 創建主題切換按鈕
   - 實現 JavaScript 切換邏輯

3. **設計頁首導航**
   - 遊戲中心標題
   - 主題切換按鈕
   - 搜尋框 (可選)

4. **創建遊戲網格**
   - 5個遊戲卡片
   - 響應式網格佈局
   - 懸停效果和動畫

5. **添加頁尾**
   - 版權信息
   - 連結 (關於我們、隱私政策等)

6. **測試與優化**
   - 測試所有遊戲連結
   - 測試主題切換功能
   - 測試響應式設計
   - 跨瀏覽器兼容性測試

## 設計參考

### 從現有主題檔案提取的元素
1. **深色模式** (anson_game_center_-_dark_mode/code.html):
   - 漸變背景: `linear-gradient(135deg, #1a1a2e 0%, #16213e 100%)`
   - 卡片背景: `rgba(45, 45, 68, 0.8)`
   - 主要顏色: `#4ecdc4`, `#ff6b6b`

2. **淺色模式** (anson_game_center_-_light_mode/code.html):
   - 漸變背景: `linear-gradient(to bottom, #f0f8ff, #e6f7ff)`
   - 卡片背景: `rgba(255, 255, 255, 0.9)`
   - 主要顏色: `#ffa500`, `#4CAF50`

## 成功標準
1. ✅ 所有 5 個遊戲都能從 index.html 訪問
2. ✅ 深色/淺色主題切換功能正常
3. ✅ 響應式設計在各種設備上正常顯示
4. ✅ 設計風格與現有遊戲保持一致
5. ✅ 頁面加載速度快，性能良好

## 下一步行動
1. 創建 index.html 檔案
2. 實現主題切換功能
3. 添加遊戲卡片
4. 測試所有功能
5. 部署到生產環境