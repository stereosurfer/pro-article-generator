# Phase 1: Multilingual Search / 多語系搜尋

> Phase 1 of 7 — Research Workflow v2.0

---

## Prerequisites / 前置條件

- **Must read first**: `outputs/{slug}/checkpoint-0.md`
- **Must load**: `categories/{category}/search-templates.md`
- **Must load**: `categories/{category}/trusted-media.md`
- **Must load**: `categories/{category}/trusted-forums.md`
- **Must load**: `categories/{category}/trusted-technical.md`

---

## Output / 產出

- **File**: `outputs/{slug}/sources.md`
- **Minimum sources**: ≥ 20 (after all rounds)
- **Incremental save**: After EACH round (R1, R2, R3, R4)

---

## Task Instructions / 任務指令

### Preparation / 準備

1. Read `checkpoint-0.md` to get product name, category, and origin language
2. Read `search-templates.md` to get query templates for this category
3. Read `trusted-media.md`, `trusted-forums.md`, `trusted-technical.md` to know which sources to prioritize

### Round 1: Official & Technical Documentation / 第 1 輪：官方與技術文件

**Goal**: Establish the technical foundation. Target L1 sources.
**目標**: 建立技術主幹。目標 L1 來源。

1. Substitute `{brand}` and `{model}` into Round 1 templates from `search-templates.md`
   將 `{brand}` 和 `{model}` 代入搜尋模板

2. Execute each search query using `search_web` tool
   使用 `search_web` 工具執行每個搜尋查詢

3. For each result, record:
   為每個結果記錄：
   - URL
   - Title
   - Language
   - Round (R1)
   - Preliminary evidence level (L1/L2/L3/L4 — based on source type)
   - Relevance summary (1 sentence)

4. **SAVE IMMEDIATELY**: Write/append to `sources.md` after R1 completes
   **立即保存**：R1 完成後寫入 sources.md

### Round 2: Professional Media Reviews / 第 2 輪：專業媒體評測

**Goal**: Gather expert analysis, measurements, subjective impressions. Target L2 sources.
**目標**: 收集專家分析、量測、主觀印象。目標 L2 來源。

1. Use Round 2 templates + origin language supplement queries
2. Prioritize sources listed in `trusted-media.md`
3. For origin-country equipment, add queries in origin language
4. **SAVE**: Append R2 results to `sources.md`

### Round 3: Professional Community Discussions / 第 3 輪：專業社群討論

**Goal**: Collect community consensus, modification experience, failure modes. Target L3 sources.
**目標**: 收集社群共識、改裝經驗、故障模式。目標 L3 來源。

1. Use Round 3 templates
2. Prioritize forums listed in `trusted-forums.md`
3. Apply forum selection rules (thread length, named professionals, recency)
4. **SAVE**: Append R3 results to `sources.md`

### Round 4: Market & Pricing / 第 4 輪：市場與價格

**Goal**: Support Chapter 7 market value analysis. Target L2-L3 sources.
**目標**: 支持第 7 章市場價值分析。目標 L2-L3 來源。

1. Use Round 4 templates
2. Record pricing data with: platform, query date, currency, condition
3. **SAVE**: Append R4 results to `sources.md`, update final statistics

---

## Output Format / 輸出格式

```markdown
# Phase 1: Sources / 來源清單

## Product: {brand} {model}
## Category: {category}

---

## R1: Official & Technical / 官方與技術文件

| # | URL | Title | Lang | Level | Relevance |
|---|-----|-------|------|-------|-----------|
| 1 | https://... | ... | EN | L1 | ... |

## R2: Professional Media / 專業媒體

| # | URL | Title | Lang | Level | Relevance |
|---|-----|-------|------|-------|-----------|
| N+1 | https://... | ... | EN | L2 | ... |

## R3: Community Discussions / 社群討論

| # | URL | Title | Lang | Level | Relevance |
|---|-----|-------|------|-------|-----------|

## R4: Market & Pricing / 市場價格

| # | URL | Title | Lang | Level | Relevance |
|---|-----|-------|------|-------|-----------|

---
## 📊 Phase 1 Statistics / Phase 1 統計
- Total sources found / 找到來源總數: {N}
- Rounds completed / 已完成搜尋輪數: R1, R2, R3, R4
- By level / 依等級: L1={n}, L2={n}, L3={n}, L4={n}
- By language / 依語系: EN={n}, JP={n}, ZH={n}, DE={n}, Other={n}
- Phase start time / 開始時間: {ISO 8601}
- Phase end time / 結束時間: {ISO 8601}
- Next phase / 下一步: Phase 1.5 (URL Audit / URL 審計)
- Resume instruction / 恢復指令: If resuming, check which rounds are completed above and continue from next round / 若恢復，檢查上方已完成的輪數，從下一輪繼續
```

---

## Success Signal / 成功訊號

```
✅ Phase 1 complete / Phase 1 完成
   ├── Output: sources.md ({N} sources, {L} lines)
   ├── Rounds: R1 ✅ R2 ✅ R3 ✅ R4 ✅
   ├── Sources: L1={n} L2={n} L3={n} L4={n}
   └── Next: Phase 1.5 (URL Audit)
```

## Failure Handling / 失敗處理

- Total sources < 15 after all 4 rounds → add supplementary Round 5 with broader queries / 來源 < 15 → 增加第 5 輪補充搜尋
- No L1 sources found → explicitly note in sources.md footer as "L1 gap" / 無 L1 來源 → 在統計中明確標注「L1 缺口」
