# Phase 2: Outline Planning / 大綱規劃

> Phase 2 of 7 — Research Workflow v2.0

---

## Prerequisites / 前置條件

- **Must read first**: `outputs/{slug}/audit-urls.md`
- **Must load**: `_agents/skills/researcher/standards/report-structure.md`
- **Must load**: `categories/{category}/category.md` (for chapter customizations)

---

## Output / 產出

- **File**: `outputs/{slug}/plan.md`
- **Must contain**: All 9 chapters (Chapter 0-8)
- **Each chapter must have**: ≥ 1 valid source mapped

---

## Task Instructions / 任務指令

### Step 1: Extract valid sources / 提取有效來源

From `audit-urls.md`, compile the list of all sources marked ✅ Valid.
Only use valid sources for outline planning. Ignore invalid ones.
從 `audit-urls.md` 中提取所有標記 ✅ 的有效來源。

### Step 2: Load report structure / 載入報告結構

Read `standards/report-structure.md` to get the 9-chapter template.
Read `categories/{category}/category.md` to get chapter customizations for this category.
載入通用報告結構和品類客製化設定。

### Step 3: Map sources to chapters / 來源映射到章節

For each chapter (0-8):
對每個章節（0-8）：

1. Identify which valid sources are relevant to this chapter
2. Assign evidence levels based on source type
3. Estimate planned paragraph count
4. Note any key claims that can be made based on available sources
5. Identify gaps (chapters with no L1-L2 sources)

### Step 4: Gap analysis / 缺口分析

For any chapter with:
- No sources at all → Mark as "⚠️ DATA GAP — will include blind spot declaration"
- Only L3-L4 sources → Mark as "⚠️ LOW EVIDENCE — community consensus only"
- No L1 sources → Note for Phase 2.5 attention

### Step 5: Write plan.md / 寫入 plan.md

---

## Output Format / 輸出格式

```markdown
# Phase 2: Report Outline / 報告大綱

## Product: {brand} {model}
## Based on: {N} valid sources from audit-urls.md

---

## Chapter 0: Executive Summary / 執行摘要
- **Sources**: [#{id}][L{level}] {url}, ...
- **Planned paragraphs**: {N}
- **Key content**: {brief description}

## Chapter 1: Historical Lineage & Design Philosophy / 歷史背景與設計哲學
- **Sources**: [#{id}][L{level}] {url}, ...
- **Planned paragraphs**: {N}
- **Key claims**:
  - {claim 1} (supported by source #{id}, L{level})
  - {claim 2} ...
- **Gaps**: {any gaps noted}

## Chapter 2: Technical Architecture / 技術架構
(same structure...)

... (Chapters 3-7 same structure)

## Chapter 8: Research Statistics / 研究統計
- **Sources**: all
- **Planned paragraphs**: 3
- **Content**: Source matrix, audit results summary, blind spot declaration

---
## Overall Gap Summary / 整體缺口摘要
- Chapters with L1 coverage: {list}
- Chapters with gaps: {list}
- Recommended actions: {any supplementary search needed}

---
## 📊 Phase 2 Statistics / Phase 2 統計
- Chapters planned / 規劃章節數: 9
- Chapters with ≥1 source / 有來源的章節: {N}/9
- Chapters with L1 source / 有 L1 來源的章節: {N}/9
- Total planned paragraphs / 預計總段落數: {N}
- Gaps identified / 識別到的資料缺口: {N}
- Phase start time / 開始時間: {ISO 8601}
- Phase end time / 結束時間: {ISO 8601}
- Next phase / 下一步: Phase 2.5 (Claims Audit / 引用審計)
- Resume instruction / 恢復指令: Skip Phase 2, proceed to Phase 2.5 / 跳過 Phase 2，直接進入 Phase 2.5
```

---

## Success Signal / 成功訊號

```
✅ Phase 2 complete / Phase 2 完成
   ├── Output: plan.md ({N} lines)
   ├── Chapters: 9/9 planned
   ├── L1 coverage: {N}/9 chapters
   └── Next: Phase 2.5 (Claims Audit)
```

## Failure Handling / 失敗處理

- If > 3 chapters have no sources → return to Phase 1 for supplementary search / 超過 3 章無來源 → 回 Phase 1 補搜
- If Chapter 2 (Technical) has no L1 source → flag as critical gap / 第 2 章(技術)無 L1 來源 → 標記為關鍵缺口
