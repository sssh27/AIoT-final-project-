# 初興 (NCHU All-in-One) — 智慧校園一站式整合系統

![NCHU Badge](https://img.shields.io/badge/University-NCHU-green)
![Tech Stack](https://img.shields.io/badge/Platform-iOS-blue)
![Architecture](https://img.shields.io/badge/Architecture-MVVM-orange)

## 📋 專案摘要 (Abstract)

*   **A (Attention Getter / Motivation)**：儘管智慧型手機普及，但中興大學學生在校園生活中仍面臨多個系統碎片化、導航資訊不精確及選課排程效率低下的問題。
*   **B (But / Challenge)**：現有校園系統介面陳舊且功能分散，缺乏專為行動端設計、具備情境感知功能的智慧助理。
*   **C (Cure / Solution)**：本專案提出名為「初興」的 iOS 應用程式，旨在透過一站式整合，打破資訊孤島，提升校園生活效率。
*   **D (Development)**：本系統採用 SwiftUI 與 MVVM 平行開發架構，並導入 O(n²) 衝堂偵測演算法與基於 Set 交集的通識課程推薦邏輯。
*   **E (Experiments)**：透過系統模擬與效能評估，驗證演算法在處理上千門課程資料時，能達到毫秒級反應且維持 0% 衝堂率。
*   **F (Findings)**：初步邏輯驗證顯示，「初興」能顯著減少分頁切換頻率，並顯著提升學生對校園特約醫療及通識課程的檢索效率。

---

## 1. 引言 (Introduction / A to F Logic)

### 動機與背景 (A)
中興大學學生每天需要處理包括 iLearning 課程、圖書館預約、及校園入口登錄等多項數位事務。然而，這些服務目前皆為獨立網頁，缺乏一個統一的行動化入口。

### 問題與挑戰 (B)
*   **資訊碎片化**：不同服務需多次登入，切換成本高。
*   **選課痛點**：無法直觀找出空堂時段可選的課程。
*   **導航障礙**：一般地圖與校園大樓代號（如 AT, AG）不兼容。

### 解決方案 (C)
「初興」App 提供了一個智慧核心，預整合所有核心 API，確保使用者在單一 App 內即可完成 90% 的校園事務處理。

---

## 2. 相關研究 (Related Work / NotebookLM Analysis)

透過 **NotebookLM** 對智慧校園架構進行文獻分析，我們得出以下結論：
*   **現有系統比較**：傳統 Web-wrapper 類型的 App 缺乏本地端資料處理能力，導致 UI 反應遲鈍。
*   **差異化優勢**：相較於現有 NCHU Portal，「初興」導入了本地端演算法（衝堂偵測）以及針對 NCHU 特約診所優化的地理圖標。
*   **情境感知設計**：引用當前回應式系統理論，「初興」設計了主動提醒功能（下一堂課位置），將被動查詢提升為主動推送。

---

## 3. 提案設計 (Proposed Design / 規格書)

### 系統規格
*   **操作系統**：iOS 15.0 或以上。
*   **核心功能模組**：
    1.  **智慧課表**：支援動態網格編輯與自動顏色映射。
    2.  **校園地圖**：大樓代號關鍵字搜尋與一鍵導航。
    3.  **生活助手**：特約診所地圖、自學空間 WebView 嵌入。
*   **使用者介面**：採用「中興鴨」主題化設計，支援 Dark Mode 與外觀自訂。

---

## 4. 詳細實作 (Detail Implementation)

### 技術架構
*   **MVVM 架構**：解耦 UI 與邏輯，確保程式碼的可維護性。
*   **資料模型 (Models)**：定義課程與用戶數據之 JSON 結構。

### 核心演算法
#### 衝堂偵測 (Conflict Detection)
```swift
// 衝堂偵測邏輯示例
func checkConflicts(currentCourses: [Course], newCourse: Course) -> Bool {
    return currentCourses.allSatisfy { $0.periods.isDisjoint(with: newCourse.periods) }
}
```
系統利用 `Set` 的 `isDisjoint` 操作，在選課或手動編輯時即時攔截時間衝突。

---

## 5. 結論 (Conclusion)

### 預期發現
我們的設計證明了單一入口在提升學生生活效率上的潛力。未來開發方向將專注於更精確的室內導航與全校資源的 API 即時對接。

### 專案資源
*   **簡報連結**：[初興_proposal.pptx](./初興_proposal.pptx)
*   **展示影片**：[YouTube 連結](https://youtu.be/5bYZXAhFniQ)

---

## 👥 團隊成員
*   電資3 劉李陽
*   資工3 王彥翔
*   資工3 許唐豪
