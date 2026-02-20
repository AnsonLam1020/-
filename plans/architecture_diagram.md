# Anson Game Center 系統架構圖

## 系統架構概覽

```mermaid
graph TB
    subgraph "前端層 Frontend Layer"
        A[index.html - 遊戲中心入口]
        B[shared.css - 共享樣式]
        C[theme-toggle.js - 主題切換]
        
        subgraph "遊戲模塊 Game Modules"
            D[game1.html - 貪食蛇]
            E[game2.html - 彈跳方塊]
            F[game3.html - 包剪揼]
            G[game4.html - 極速賽車]
            H[game5.html - 密室逃脫]
        end
    end
    
    subgraph "設計系統 Design System"
        I[深色模式 Dark Theme]
        J[淺色模式 Light Theme]
        K[響應式佈局 Responsive Layout]
        L[遊戲卡片組件 Game Card Component]
    end
    
    subgraph "用戶體驗 UX"
        M[主題切換 Theme Toggle]
        N[遊戲分類 Game Categories]
        O[搜尋功能 Search]
        P[遊戲篩選 Filter]
    end
    
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    
    B --> I
    B --> J
    B --> K
    B --> L
    
    C --> M
    
    I --> A
    J --> A
    K --> A
    L --> A
    
    M --> A
    N --> A
    O --> A
    P --> A
```

## 頁面結構流程圖

```mermaid
flowchart TD
    Start[用戶訪問 index.html] --> CheckTheme{檢查主題偏好}
    CheckTheme -->|本地存儲有主題| LoadTheme[加載保存的主題]
    CheckTheme -->|無保存主題| DefaultTheme[使用深色模式]
    
    LoadTheme --> RenderPage[渲染頁面]
    DefaultTheme --> RenderPage
    
    RenderPage --> ShowHeader[顯示頁首]
    ShowHeader --> ShowHero[顯示特色遊戲區]
    ShowHero --> ShowCategories[顯示遊戲分類]
    ShowCategories --> ShowGames[顯示遊戲網格]
    ShowGames --> ShowFooter[顯示頁尾]
    
    ShowFooter --> UserInteraction{用戶交互}
    
    UserInteraction -->|點擊主題切換| ToggleTheme[切換主題]
    UserInteraction -->|點擊遊戲卡片| NavigateGame[導航到遊戲]
    UserInteraction -->|點擊分類標籤| FilterGames[篩選遊戲]
    UserInteraction -->|使用搜尋框| SearchGames[搜尋遊戲]
    
    ToggleTheme --> SaveTheme[保存主題偏好]
    SaveTheme --> UpdateUI[更新UI]
    UpdateUI --> UserInteraction
    
    NavigateGame --> OpenGame[打開遊戲頁面]
    FilterGames --> UpdateGrid[更新遊戲網格]
    SearchGames --> UpdateGrid
    
    UpdateGrid --> UserInteraction
```

## 響應式設計斷點

```mermaid
graph LR
    subgraph "設備響應式設計"
        A[超小屏幕 < 480px] -->|1列佈局| A1[遊戲卡片: 全寬]
        B[小屏幕 480px-768px] -->|2列佈局| B1[遊戲卡片: 50%寬度]
        C[中等屏幕 768px-1024px] -->|3列佈局| C1[遊戲卡片: 33.33%寬度]
        D[大屏幕 1024px-1440px] -->|4列佈局| D1[遊戲卡片: 25%寬度]
        E[超大屏幕 > 1440px] -->|5列佈局| E1[遊戲卡片: 20%寬度]
    end
    
    subgraph "組件響應式行為"
        F[導航欄] -->|移動設備| F1[漢堡菜單]
        F -->|桌面設備| F2[水平導航]
        G[搜尋框] -->|移動設備| G1[隱藏/圖標]
        G -->|桌面設備| G2[顯示搜索框]
        H[遊戲卡片] -->|移動設備| H1[簡化內容]
        H -->|桌面設備| H2[完整內容]
    end
```

## 主題切換機制

```mermaid
sequenceDiagram
    participant User as 用戶
    participant Button as 主題切換按鈕
    participant JS as JavaScript
    participant CSS as CSS變數
    participant Storage as 本地存儲
    
    User->>Button: 點擊主題切換
    Button->>JS: 觸發 toggleTheme()
    JS->>CSS: 讀取當前主題
    CSS-->>JS: 返回 'dark' 或 'light'
    JS->>CSS: 設置新主題變數
    JS->>Storage: 保存主題偏好
    Storage-->>JS: 確認保存
    JS->>CSS: 應用新主題樣式
    CSS-->>User: 更新頁面外觀
```

## 遊戲卡片組件結構

```mermaid
classDiagram
    class GameCard {
        +String icon
        +String title
        +String description
        +Array tags
        +String link
        +render()
        +handleClick()
    }
    
    class GameGrid {
        +Array games
        +String layout
        +renderCards()
        +filterByCategory()
        +searchGames()
    }
    
    class ThemeManager {
        +String currentTheme
        +toggleTheme()
        +savePreference()
        +loadPreference()
    }
    
    GameGrid "1" *-- "*" GameCard : contains
    ThemeManager --> GameCard : applies theme
    ThemeManager --> GameGrid : applies theme
```

## 文件依賴關係

```mermaid
graph TD
    index.html --> shared.css
    index.html --> theme-toggle.js
    index.html --> game1.html
    index.html --> game2.html
    index.html --> game3.html
    index.html --> game4.html
    index.html --> game5.html
    
    shared.css --> dark-theme.css
    shared.css --> light-theme.css
    
    theme-toggle.js --> localStorage
    
    subgraph "外部資源 External Resources"
        GoogleFonts[Google Fonts]
        MaterialIcons[Material Icons]
        TailwindCSS[Tailwind CSS - 可選]
    end
    
    index.html --> GoogleFonts
    index.html --> MaterialIcons
    index.html --> TailwindCSS
```

## 實施優先級

```mermaid
gantt
    title Anson Game Center 實施時間線
    dateFormat YYYY-MM-DD
    section 核心功能
    基礎HTML結構 :2026-02-20, 1d
    主題系統實現 :2026-02-21, 1d
    遊戲卡片組件 :2026-02-21, 1d
    響應式設計 :2026-02-22, 1d
    
    section 增強功能
    主題切換動畫 :2026-02-22, 0.5d
    遊戲分類篩選 :2026-02-23, 0.5d
    搜尋功能 :2026-02-23, 0.5d
    
    section 測試優化
    跨瀏覽器測試 :2026-02-24, 1d
    性能優化 :2026-02-24, 0.5d
    最終驗收 :2026-02-25, 0.5d
```

## 技術決策點

1. **CSS 框架選擇**
   - 選項 A: 純 CSS + 自定義變數
   - 選項 B: Tailwind CSS (現有主題使用)
   - 推薦: 使用現有 Tailwind CSS 配置保持一致性

2. **主題存儲策略**
   - 選項 A: localStorage
   - 選項 B: cookies
   - 選項 C: 服務器端存儲
   - 推薦: localStorage (簡單有效)

3. **響應式斷點**
   - 基於現有遊戲的斷點設計
   - 保持一致的用户體驗

4. **瀏覽器兼容性**
   - 目標: Chrome, Firefox, Safari, Edge
   - 最低支援: ES6, CSS Grid, Flexbox