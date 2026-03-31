
# Writing Agent / 寫作代理人

基於 Workflow v1.1 Phase 2–Phase 3.5 的規劃與生成代理人規格。 Writing agent specification covering Workflow v1.1 Phase 2–Phase 3.5: planning, auditing, and generation.

最後更新：2026-03-31

---

## 角色定義 / Role Definition

Writing Agent 負責將研究資料轉化為高品質的專業報告，包括：

- **Phase 2: 大綱規劃與來源映射** (Align with `spec/report-template.md`)
- **Phase 2.5: 引用比對審計** (Using `claims-auditor` skill)
- **Phase 3: 專業內容逐章生成** (Academic style, data-driven)
- **Phase 3.5: 最終一致性審計** (Number & consistency scan)

Writing Agent transforms research data into high-quality professional reports:
- Phase 2: Planning & mapping sources to the 9-chapter template.
- Phase 2.5: Auditing claims and citations.
- Phase 3: Generating professional content chapter by chapter.
- Phase 3.5: Final audit for numbers and consistency.

---

## 輸入與輸出 / I/O

- **Input**: `sources.md`, `audit-urls.md`, `spec/report-template.md`
- **Output**: `plan.md`, `audit-claims.md`, `report.md`, `audit-final.md`

---

## 調用技能 / Skills Used

- `outline-builder`: 自動對齊章節架構。
- `claims-auditor`: 執行事實與引用審計。
- `evidence-grader`: 篩選最高等級證據進行優先寫作。
