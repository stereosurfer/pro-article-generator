# Phase 3: Report Generation / 報告生成

> Phase 3 of 7 — Research Workflow v2.0

---

## Prerequisites / 前置條件

- **Must read first**: `outputs/{slug}/audit-claims.md`
- **Must load**: `_agents/skills/researcher/standards/evidence-levels.md`

---

## Output / 產出

- **File**: `outputs/{slug}/report.md`
- **Minimum word count**: ≥ 5,000 words (combined EN + ZH)
- **Incremental save**: After each chapter completed
- **MUST split into 3 sub-phases** (see §5 of SKILL.md)

---

## ⚠️ CRITICAL: Sub-Phase Context Control / 分段上下文控制

Phase 3 is the most context-intensive phase. It MUST be split:
Phase 3 是最耗上下文的階段，必須分段：

```
P3a: Generate Chapter 0, 1, 2 → write to report.md
P3b: Generate Chapter 3, 4, 5 → append to report.md
P3c: Generate Chapter 6, 7, 8 → append to report.md
```

**Between sub-phases**: Only retain chapter TITLES of previously generated chapters, not full text. Re-read `audit-claims.md` for the relevant chapters only.
**子階段之間**：僅保留已生成章節的「標題」，不保留全文。僅重新讀取 audit-claims.md 中相關章節的部分。

---

## Task Instructions / 任務指令

### For each chapter / 對每個章節：

1. **Read claims** — Find all VERIFIED claims for this chapter from `audit-claims.md`
   讀取 audit-claims.md 中此章節所有 VERIFIED 的主張

2. **Read sources** — For key claims, use `read_url_content` to get detailed content from the source URLs
   對關鍵主張，用 `read_url_content` 取得來源的詳細內容

3. **Write bilingual content** — Follow this format:
   撰寫雙語內容 — 遵循以下格式：

```markdown
## {Chapter}.{Section} {English Title}
## {Chapter}.{Section} {中文標題}

{English paragraph with inline evidence tags and source URLs.
Every factual claim must include [L{level}: {source description}].}

{對應的中文段落，同樣的證據標注和來源引用。
每個事實主張必須包含 [L{等級}: {來源說明}]。}
```

4. **Handle UNVERIFIED claims** — If a claim from plan.md was marked UNVERIFIED in audit-claims.md:
   處理未驗證的主張：
   - Include it ONLY if necessary for narrative flow / 僅在敘述需要時納入
   - MUST append: "(This claim could not be independently verified from the cited source.)" / 必須附加未驗證聲明
   - "(此主張無法從引用來源獨立驗證。)"

5. **Handle CONFLICT claims** — If a claim was marked CONFLICT:
   處理衝突主張：
   - Present BOTH versions from the sources / 呈現來源的兩個版本
   - Explain the discrepancy / 說明差異原因
   - Do NOT arbitrarily choose one / 不得任意選擇其一

6. **Save after each chapter** — Append the completed chapter to `report.md`
   每完成一章，追加到 report.md

---

## Writing Style Rules / 寫作風格規則

1. **Academic but accessible** — Professional tone, clear structure, avoid jargon without explanation
   學術但可讀 — 專業語調，清晰結構，避免未解釋的術語

2. **Data-driven** — Every factual statement needs an evidence tag
   以數據為本 — 每個事實陳述需要證據標注

3. **Bilingual parity** — Chinese paragraphs must convey the same technical detail as English, not simplified summaries
   雙語對等 — 中文段落必須傳達與英文相同的技術細節，不是簡化摘要

4. **Uncertainty honesty** — Clearly mark speculative vs. verified content
   不確定性誠實 — 清楚標明推測 vs. 已驗證的內容

---

## Output Format / 輸出格式

```markdown
# {Product Name}: Research Report
# {產品名稱}：研究報告

> Generated: {date} | Category: {category} | System: v1.0
> 生成日期：{date} | 品類：{category} | 系統版本：v1.0

---

## Chapter 0: Executive Summary / 執行摘要
(content...)

## Chapter 1: Historical Lineage / 歷史背景
(content...)

... (all 9 chapters)

---
## 📊 Phase 3 Statistics / Phase 3 統計
- Chapters generated / 已生成章節: 9/9
- Total word count / 總字數: {N} (EN: {n}, ZH: {n})
- Evidence tags used / 證據標注數: {N}
- Sub-phases completed / 已完成子階段: P3a ✅ P3b ✅ P3c ✅
- UNVERIFIED claims included / 納入的未驗證主張: {N}
- CONFLICT claims handled / 處理的衝突主張: {N}
- Phase start time / 開始時間: {ISO 8601}
- Phase end time / 結束時間: {ISO 8601}
- Next phase / 下一步: Phase 3.5 (Final Audit / 最終審計)
- Resume instruction / 恢復指令: Check which chapters exist in report.md. Resume from next missing chapter. / 檢查 report.md 中已有哪些章節，從下一個缺少的章節繼續。
```

---

## Success Signal / 成功訊號

```
✅ Phase 3 complete / Phase 3 完成
   ├── Output: report.md ({N} lines, {W} words)
   ├── Chapters: 9/9 generated
   ├── Evidence tags: {N}
   └── Next: Phase 3.5 (Final Audit)
```
