# Phase 2.5: Claims Audit / 引用審計

> Phase 2.5 of 7 — Research Workflow v2.0

---

## Prerequisites / 前置條件

- **Must read first**: `outputs/{slug}/plan.md`
- **Must load**: `_agents/skills/researcher/standards/evidence-levels.md`

---

## Output / 產出

- **File**: `outputs/{slug}/audit-claims.md`

---

## Task Instructions / 任務指令

### Step 1: Extract claims from plan.md / 從 plan.md 提取主張

Read `plan.md` and extract every factual claim listed under "Key claims" for each chapter.
讀取 `plan.md`，提取每個章節的所有事實主張。

### Step 2: Verify each claim / 驗證每個主張

For each claim:
對每個主張：

1. **Identify the cited source** — which URL and evidence level supports this claim?
   識別引用來源 — 哪個 URL 和證據等級支持這個主張？

2. **Cross-reference** — Use `read_url_content` on the source URL to verify the claim appears in the actual page content.
   交叉比對 — 用 `read_url_content` 讀取來源 URL 驗證主張是否出現在實際頁面內容中。

3. **Classify the result** / 分類結果：
   - **✅ VERIFIED**: Claim matches source content / 主張與來源內容一致
   - **⚠️ UNVERIFIED**: Cannot confirm from source (content changed, paywalled, or claim not found) / 無法從來源確認
   - **❌ CONFLICT**: Source says something different from the claim / 來源與主張矛盾

4. **Check evidence level appropriateness** — Per `evidence-levels.md`, is the claim strength appropriate for its evidence level?
   檢查證據等級是否適當 — 依據 `evidence-levels.md`，主張強度是否與證據等級匹配？
   - E.g., precise specs claimed with only L3 source → flag as "needs L1 source"

### Step 3: Calculate verification rate / 計算驗證率

```
Verification rate = VERIFIED count / Total claims
```

If UNVERIFIED > 30% → trigger backtrack rule (see below)

### Step 4: Write audit-claims.md / 寫入 audit-claims.md

---

## Output Format / 輸出格式

```markdown
# Phase 2.5: Claims Audit / 引用審計結果

## Product: {brand} {model}

---

## Audit Results / 審計結果

| # | Chapter | Claim | Source | Level | Status | Notes |
|---|---------|-------|--------|-------|--------|-------|
| 1 | Ch1 | {claim text} | [#{id}] {url} | L1 | ✅ VERIFIED | {notes} |
| 2 | Ch2 | {claim text} | [#{id}] {url} | L2 | ⚠️ UNVERIFIED | {reason} |
| 3 | Ch3 | {claim text} | [#{id}] {url} | L3 | ❌ CONFLICT | {what source says vs claim} |

## Level Appropriateness Flags / 證據等級適當性標記

| # | Claim | Current Level | Required Level | Action |
|---|-------|--------------|----------------|--------|
| 1 | {precise spec claimed} | L3 | L1 | Must find L1 source or add uncertainty note |

---
## 📊 Phase 2.5 Statistics / Phase 2.5 統計
- Total claims audited / 審計主張總數: {N}
- VERIFIED / 已驗證: {N} ({%})
- UNVERIFIED / 未驗證: {N} ({%})
- CONFLICT / 衝突: {N} ({%})
- Level mismatches / 等級不匹配: {N}
- Backtrack triggered / 觸發回溯: {Yes/No}
- Phase start time / 開始時間: {ISO 8601}
- Phase end time / 結束時間: {ISO 8601}
- Next phase / 下一步: Phase 3 (Report Generation) OR Phase 1 (Backtrack)
- Resume instruction / 恢復指令: {instructions}
```

---

## Backtrack Rule / 回溯規則

If UNVERIFIED claims > 30%:
若 UNVERIFIED > 30%：

1. Report: "⚠️ Verification rate {N}% below 70% threshold."
2. Ask user: "Return to Phase 1 for supplementary search, or proceed with uncertainty notes?"
3. If backtrack → run Phase 1 supplement, then re-run Phase 1.5, Phase 2, Phase 2.5
4. If proceed → add uncertainty notes to all UNVERIFIED claims in Phase 3

---

## Success Signal / 成功訊號

```
✅ Phase 2.5 complete / Phase 2.5 完成
   ├── Output: audit-claims.md ({N} lines)
   ├── Verified: {N}/{total} ({%})
   └── Next: Phase 3 (Generate)
```
