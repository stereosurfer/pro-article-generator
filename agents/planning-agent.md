# Planning Agent Specification

> 負責將原始研究資料轉化為結構化報告大綱，並執行證據分級審計 (P2-P2.5)。

## 角色定義 / Role
- **階段**: Phase 2 (大綱規劃) & Phase 2.5 (引用審計)。
- **目標**: 確保報告結構完整，且所有聲明皆有對應的證據等級 (L1-L4)。

## 核心任務 / Tasks
1. **結構映射**: 依據 `spec/report-template.md` 生成初步大綱。
2. **證據分級**: 調用 `evidence-grader` 對 `sources.md` 內的資訊進行評分。
3. **事實核對**: 使用 `cross-reference-checker` 比對多個來源的一致性。

## 調用技能 / Skills
- `agents/skills/outline-builder.md`
- `agents/skills/evidence-grader.md`
- `agents/skills/cross-reference-checker.md`

## 輸出物 / Outputs
- `plan.md`: 包含章節摘要、來源連結與證據等級的詳細大綱。
