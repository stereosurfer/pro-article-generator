# Phase 1.5: URL Audit / URL 審計

> Phase 1.5 of 7 — Research Workflow v2.0

---

## Prerequisites / 前置條件

- **Must read first**: `outputs/{slug}/sources.md`
- **No additional files needed** (sources.md contains all URLs to audit)

---

## Output / 產出

- **File**: `outputs/{slug}/audit-urls.md`
- **Incremental save**: After every 5 URLs verified

---

## Task Instructions / 任務指令

### Step 1: Extract all URLs from sources.md / 從 sources.md 提取所有 URL

Read `sources.md` and compile a list of all URLs to audit.
讀取 `sources.md`，彙整所有需要審計的 URL。

### Step 2: Audit each URL / 逐一審計每個 URL

For each URL, perform these checks using `read_url_content`:
用 `read_url_content` 對每個 URL 執行以下檢查：

#### Check A: Reachability / 可存取性 (MANDATORY)
- Can the URL be accessed? / URL 能否存取？
- If `read_url_content` returns content → ✅ Reachable
- If it fails or returns error → ❌ Unreachable

#### Check B: Relevance / 相關性 (Weight: 40%)
- Does the returned content actually mention the target product? / 回傳的內容是否確實提及目標產品？
- Search for brand name AND model number in the content
- Score: 0.0 (no mention) to 1.0 (primary topic)

#### Check C: Recency / 時效性 (Weight: 20%)
- When was the content published or last updated? / 內容何時發表？
- Prefer sources within 2 years; accept within 10 years
- Score: 1.0 (< 2 years) / 0.7 (2-5 years) / 0.5 (5-10 years) / 0.3 (> 10 years)

#### Check D: Authority / 權威性 (Weight: 40%)
- Is this source in the trusted media, forums, or technical lists? / 此來源是否在信任清單中？
- Score: 1.0 (in Tier 1 trusted list) / 0.7 (Tier 2) / 0.5 (professional but not listed) / 0.2 (general)

### Step 3: Calculate composite score / 計算綜合分數

```
Score = (Relevance × 0.4) + (Recency × 0.2) + (Authority × 0.4)
Valid if: Reachable AND Score ≥ 0.5
```

### Step 4: Incremental save / 增量保存

After every 5 URLs audited, append results to `audit-urls.md`.
每審計 5 個 URL，追加結果到 `audit-urls.md`。

### Step 5: Final assessment / 最終評估

Count valid sources. If valid < 20 → trigger backtrack to Phase 1.
統計有效來源數量。若有效 < 20 → 觸發回溯到 Phase 1。

---

## Output Format / 輸出格式

```markdown
# Phase 1.5: URL Audit Results / URL 審計結果

## Product: {brand} {model}

---

## Audit Results / 審計結果

| # | URL | Reachable | Relevance | Recency | Authority | Score | Status | Reason |
|---|-----|-----------|-----------|---------|-----------|-------|--------|--------|
| 1 | https://... | ✅ | 0.95 | 0.8 | 1.0 | 0.94 | ✅ Valid | Official doc |
| 2 | https://... | ❌ | — | — | — | — | ❌ Invalid | HTTP error |

---
## 📊 Phase 1.5 Statistics / Phase 1.5 統計
- Total audited / 審計總數: {N}
- Valid / 有效: {N} (score ≥ 0.5)
- Invalid / 無效: {N}
- Valid rate / 有效率: {N}%
- Backtrack triggered / 觸發回溯: {Yes/No}
- Phase start time / 開始時間: {ISO 8601}
- Phase end time / 結束時間: {ISO 8601}
- Next phase / 下一步: Phase 2 (Outline Planning) OR Phase 1 (Backtrack)
- Resume instruction / 恢復指令: {instructions}
```

---

## Backtrack Rule / 回溯規則

If valid sources < 20:
若有效來源 < 20：

1. Report: "⚠️ Only {N} valid sources. Minimum is 20. Returning to Phase 1 for supplementary search."
2. Go back to Phase 1, run additional search queries with modified/broader terms
3. Re-run Phase 1.5 on new sources

---

## Success Signal / 成功訊號

```
✅ Phase 1.5 complete / Phase 1.5 完成
   ├── Output: audit-urls.md ({N} lines)
   ├── Valid: {N} / Invalid: {N} ({rate}%)
   └── Next: Phase 2 (Outline)
```
