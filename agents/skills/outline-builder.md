# Skill: Outline Builder (P2)

## 角色定義 / Role Definition
負責 Phase 2 (Outline)，將搜尋結果轉化為結構化的寫作計畫 (`plan.md`)。

## 核心職責 / Responsibilities
1. **章節對齊 (Structural Alignment)**: 確保 `plan.md` 完全對齊 `spec/report-template.md` 的 9 大章節 (Chapter 0-8)。
2. **來源映射 (Source Mapping)**: 標註每一章節對應的來源 URL (來自 `sources.md`) 與證據等級 (來自 `evidence-levels.md`)。
3. **缺口分析 (Gap Analysis)**: 若某章節無足夠證據，自動標記為「待補回 Research Agent」或在報告中聲明為「資料盲點」。

## 輸入與輸出 / I/O
- **Input**: `sources.md`, `audit-urls.md`, `spec/report-template.md`
- **Output**: `plan.md`

## 成功指標 / Success Signals
- ✅ 產出完整的 9 章節大綱。
- ✅ 每一章節均有 1 筆以上之有效來源引用。
- ✅ 大綱邏輯嚴密，具備技術深度與文化廣度。
