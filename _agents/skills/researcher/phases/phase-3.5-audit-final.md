# Phase 3.5: Final Audit / 最終審計

> Phase 3.5 of 7 — Research Workflow v2.0

---

## Prerequisites / 前置條件

- **Must read first**: `outputs/{slug}/report.md`
- **Must load**: `_agents/skills/researcher/standards/audit-rules.md`

---

## Output / 產出

- **File 1**: `outputs/{slug}/audit-final.md`
- **File 2**: `outputs/{slug}/metadata.yaml`

---

## Task Instructions / 任務指令

### Step 1: Number Consistency Scan / 數字一致性掃描

Scan the entire `report.md` for all numerical values (specs, dates, measurements).
掃描整個 `report.md` 中的所有數值。

For each number that appears more than once:
對每個出現多次的數字：
1. List all locations where it appears (chapter + section)
2. Verify they are identical
3. If inconsistent → flag as CONFLICT with locations and values

### Step 2: Evidence Tag Completeness / 證據標注完整性

Verify that every factual claim in `report.md` has an evidence tag `[L{level}: ...]`.
驗證每個事實主張都有證據標注。

Flag any statements that:
標記以下情況：
- Make factual claims without evidence tags / 有事實主張但無證據標注
- Use L1-level language ("precisely", "exactly") but cite L3-L4 sources / 用 L1 語氣但引用 L3-L4 來源

### Step 3: Quality Grading / 品質分級

Calculate the quality grade based on `standards/audit-rules.md`:
依據審計規則計算品質等級：

| Grade | Criteria |
|-------|---------|
| **A** | > 40% L1 sources, no number conflicts, ≥ 70% claims verified |
| **B** | > 20% L1 sources, ≤ 2 number conflicts (resolved), ≥ 70% claims verified |
| **C** | Below B criteria |

### Step 4: Blind Spot Declaration / 盲點聲明

List all structural limitations:
列出所有結構性限制：
1. Sections lacking independent lab measurement support / 缺乏獨立量測支持的部分
2. Sections relying solely on community consensus / 僅依據社群共識的部分
3. Regional markets with insufficient language coverage / 語言資料不足的區域
4. Overall credibility self-assessment / 整體可信度自評

### Step 5: Generate metadata.yaml / 生成 metadata.yaml

```yaml
product_name: "{brand} {model}"
product_slug: "{slug}"
category: "{category}"
generated_at: "{ISO 8601}"
system_version: "v1.0.0"
skill_commit: "{current git commit hash}"
evidence_summary:
  total_sources: {N}
  l1_sources: {N}
  l2_sources: {N}
  l3_sources: {N}
  l4_sources: {N}
  valid_sources: {N}
quality_grade: "{A/B/C}"
verification_rate: "{N}%"
report_language: "en+zh"
word_count: {N}
chapters_complete: {N}/9
blind_spots:
  - "{blind spot 1}"
  - "{blind spot 2}"
number_conflicts: {N}
needs_human_review: {true/false}
```

### Step 6: Write both files / 寫入兩份文件

Write `audit-final.md` and `metadata.yaml` to the output directory.

---

## Output Format for audit-final.md / 輸出格式

```markdown
# Phase 3.5: Final Audit / 最終審計結果

## Product: {brand} {model}

---

## Number Consistency Scan / 數字一致性掃描

| # | Value | Locations | Status |
|---|-------|-----------|--------|
| 1 | {number} | Ch{X}, Ch{Y} | ✅ Consistent / ❌ Conflict |

## Evidence Tag Audit / 證據標注審計

- Total factual claims: {N}
- Claims with evidence tags: {N}
- Missing tags: {N} (listed below)
- Level mismatches: {N}

## Quality Rating / 品質評級

**Overall Grade: {A/B/C}**

| Criteria | Value | Threshold | Status |
|----------|-------|-----------|--------|
| L1 source ratio | {N}% | A: >40%, B: >20% | {met/unmet} |
| Number consistency | {N}/{N} | No conflicts | {met/unmet} |
| Claim verification | {N}% | ≥ 70% | {met/unmet} |

## Blind Spots / 盲點聲明

1. {blind spot with explanation}
2. {blind spot with explanation}

## Overall Credibility / 整體可信度

{High / Medium / Low} — {reasoning}

---
## 📊 Phase 3.5 Statistics / Phase 3.5 統計
- Numbers scanned / 掃描數字數: {N}
- Conflicts found / 發現衝突: {N}
- Quality grade / 品質評級: {A/B/C}
- Needs human review / 需人工審閱: {Yes/No}
- Phase start time / 開始時間: {ISO 8601}
- Phase end time / 結束時間: {ISO 8601}
- Status / 狀態: COMPLETE ✅
- Resume instruction / 恢復指令: Research complete. No resume needed. / 研究完成，無需恢復。
```

---

## Success Signal / 成功訊號

```
✅ Phase 3.5 complete / Phase 3.5 完成
   ├── Output: audit-final.md ({N} lines)
   ├── Output: metadata.yaml
   ├── Grade: {A/B/C}
   └── Status: RESEARCH COMPLETE 🎉
```

## Post-Completion / 完成後動作

After writing both files, proceed to SKILL.md §10 (Completion):
完成後，執行 SKILL.md §10 的完成流程：
1. Update library index / 更新圖書館索引
2. Git commit + push / 提交並推送
3. Report summary to user / 向使用者報告摘要
