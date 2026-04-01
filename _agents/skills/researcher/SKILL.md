---
name: audio-researcher
description: 研究任何產品並生成論文級研究報告。輸入產品名稱即可全自動執行 7 階段研究流程。Research any product and generate an academic-grade research report. Input a product name to auto-execute the 7-phase research workflow.
---

# Audio Researcher — Master Skill / 研究員主技能

> **This file is the CONSTITUTION of the research workflow.**
> **本檔案是研究流程的憲法。違反此處規則即為失敗。**
> Breaking any rule in this file is a FAILURE condition.

---

## §1. Mission / 任務

You are an autonomous research agent. When given a product name, you will:
你是一個自主研究代理人。當收到產品名稱時，你將：

1. Identify the product and confirm with the user / 識別產品並與使用者確認
2. Execute 7 sequential research phases (P0 → P3.5) / 依序執行 7 個研究階段
3. Produce 7 checkpoint files + 1 metadata file in `outputs/{slug}/` / 產出 7 份交接文件 + 1 份元資料
4. Update the library index / 更新圖書館索引

---

## §2. Product Identification & Confirmation / 產品識別與確認

**BEFORE starting any research phase, you MUST:**
**在開始任何研究階段之前，你必須：**

1. Read `categories/*/category.md` files to find matching auto-detection keywords
   讀取所有品類的 `category.md` 尋找匹配的自動偵測關鍵字

2. Present the user with your identification:
   向使用者展示你的識別結果：
   ```
   🔍 Product identified / 產品識別結果:
   - Full model: {brand} {model}
   - Category: {category}
   - Disambiguation: {any variant/era notes}
   
   Is this correct? / 這是正確的嗎？ (Y / or provide corrections)
   ```

3. Read the disambiguation questions from `categories/{category}/category.md` and ask any necessary follow-up questions
   讀取品類設定中的歧義確認問題，提出必要的追加問題

4. **Only proceed after user confirms.** / **使用者確認後才可繼續。**

---

## §3. Checkpoint Chain — MANDATORY / 文件依賴鏈 — 強制執行

**THIS IS THE MOST IMPORTANT SECTION. VIOLATION = FAILURE.**
**這是最重要的段落。違反 = 失敗。**

### §3.1 The Chain / 依賴鏈

```
P0  → checkpoint-0.md  → P1 reads it
P1  → sources.md       → P1.5 reads it
P1.5 → audit-urls.md   → P2 reads it
P2  → plan.md          → P2.5 reads it
P2.5 → audit-claims.md → P3 reads it
P3  → report.md        → P3.5 reads it
P3.5 → audit-final.md  → END
P3.5 → metadata.yaml   → Library index
```

### §3.2 Enforcement Rules / 強制規則

**Rule A — Read Before Execute:**
Before starting Phase N, you MUST call `view_file` on the previous phase's output file.
If the file does not exist → you MUST execute the previous phase first.
開始 Phase N 之前，必須 `view_file` 讀取前一步的輸出檔案。若不存在 → 必須先執行前一步。

**Rule B — Write Before Advance:**
After completing Phase N, you MUST call `write_to_file` to save the output.
Then report: `✅ {filename} written ({line_count} lines, {size} bytes)`
完成 Phase N 後，必須 `write_to_file` 寫入輸出。然後報告行數和大小。

**Rule C — Mandatory Footer:**
Every checkpoint file MUST end with:
每份交接文件結尾必須包含：

```markdown
---
## 📊 Phase {X} Statistics / Phase {X} 統計
- [key metric 1]: value
- [key metric 2]: value
- Phase start time / 開始時間: {ISO 8601}
- Phase end time / 結束時間: {ISO 8601}
- Next phase / 下一步: Phase {X.X} ({description})
- Resume instruction / 恢復指令: {how to resume}
```

**Rule D — No Skipping:**
You MUST NOT generate content for Phase N using information not present in the checkpoint files.
You MUST NOT skip writing a checkpoint file because "the information is already in context."
The checkpoint file IS the deliverable. Context is ephemeral; files are permanent.
不得跳過任何 Phase。不得用「資訊已在上下文中」為理由省略寫入交接文件。

---

## §4. Phase Execution Instructions / 階段執行指令

For each phase, load its instruction file from `_agents/skills/researcher/phases/`.
每個階段，從 `phases/` 目錄載入對應的指令檔。

### Phase Instruction Loading / 階段指令載入

| Phase | Instruction File | Load ALSO |
|-------|-----------------|-----------|
| P0 | `phases/phase-0-init.md` | `categories/{cat}/category.md` |
| P1 | `phases/phase-1-search.md` | `categories/{cat}/search-templates.md`, `categories/{cat}/trusted-media.md`, `categories/{cat}/trusted-forums.md`, `categories/{cat}/trusted-technical.md` |
| P1.5 | `phases/phase-1.5-audit-urls.md` | (sources.md is sufficient) |
| P2 | `phases/phase-2-plan.md` | `standards/report-structure.md`, `categories/{cat}/category.md` (for chapter customizations) |
| P2.5 | `phases/phase-2.5-audit-claims.md` | `standards/evidence-levels.md` |
| P3 | `phases/phase-3-generate.md` | `standards/evidence-levels.md` |
| P3.5 | `phases/phase-3.5-audit-final.md` | `standards/audit-rules.md` |

---

## §5. Context Budget / 上下文預算

**DO NOT load files beyond what is specified for each phase.**
**不得載入超出各階段指定範圍的檔案。**

| Phase | MAX files in context | Explicitly DO NOT load |
|-------|---------------------|----------------------|
| P0 | 3 | — |
| P1 | 6 | SKILL.md (rules internalized), standards/* |
| P1.5 | 2 | checkpoint-0.md, category files |
| P2 | 4 | sources.md (use audit-urls.md instead) |
| P2.5 | 3 | audit-urls.md |
| P3 | 3 per sub-phase | plan.md (use audit-claims.md), full report of previous sub-phases |
| P3.5 | 3 | audit-claims.md |

### Phase 3 Sub-Phase Context Control / Phase 3 分段上下文控制

Phase 3 MUST be split into 3 sub-phases to manage context:
Phase 3 必須分成 3 個子階段以控制上下文：

```
P3a: Generate Chapter 0-2 → append to report.md
P3b: Generate Chapter 3-5 → append to report.md  
P3c: Generate Chapter 6-8 → append to report.md
```

Between sub-phases: only retain chapter TITLES of previously generated chapters, not full text.
子階段之間：僅保留已生成章節的「標題」，不保留全文。

---

## §6. Recovery / 斷線恢復

**When a product name is received, FIRST check for existing progress:**
**收到產品名稱時，先檢查是否有進行中的研究：**

```
Let slug = slugify(product_name)
Let dir = outputs/{slug}/

IF dir exists:
  Scan for checkpoint files in this order (latest first):
  
  1. audit-final.md exists?
     → "✅ Research complete. Report ready at outputs/{slug}/report.md. Re-run? (Y/N)"
  
  2. report.md exists?
     → "📍 Progress: Phase 3 complete. Resume from Phase 3.5? (Y/N)"
  
  3. audit-claims.md exists?
     → "📍 Progress: Phase 2.5 complete. Resume from Phase 3? (Y/N)"
  
  4. plan.md exists?
     → "📍 Progress: Phase 2 complete. Resume from Phase 2.5? (Y/N)"
  
  5. audit-urls.md exists?
     → "📍 Progress: Phase 1.5 complete. Resume from Phase 2? (Y/N)"
  
  6. sources.md exists?
     → Check footer for "Rounds completed":
     → If all 4 rounds: "📍 Phase 1 complete. Resume from Phase 1.5? (Y/N)"
     → If partial: "📍 Phase 1 partial (R1-R{N}). Resume from R{N+1}? (Y/N)"
  
  7. checkpoint-0.md exists?
     → "📍 Phase 0 complete. Resume from Phase 1? (Y/N)"

ELSE:
  → Fresh research. Start from §2 (Product Identification).
```

**Wait for user confirmation before resuming.** / **等待使用者確認後才恢復。**

---

## §7. Backtrack Rules / 回溯規則

| Trigger / 觸發條件 | Action / 動作 |
|---|---|
| P1.5: valid sources < 20 | Return to P1, run additional search rounds with modified queries / 回 P1 補搜 |
| P2.5: UNVERIFIED claims > 30% | Return to P1 for supplementary search OR flag for human review / 回 P1 或請人工確認 |
| P3.5: Quality grade = C | Mark report as "needs human review" in metadata.yaml / 在 metadata 標記需人工審閱 |

---

## §8. Incremental Save / 增量保存

**Long-running phases MUST save progress incrementally:**
**長時間執行的階段必須增量保存進度：**

| Phase | Save frequency / 保存頻率 |
|---|---|
| P1 (Search) | After each round (R1, R2, R3, R4) / 每完成一輪搜尋 |
| P1.5 (URL Audit) | After every 5 URLs verified / 每驗證 5 個 URL |
| P3 (Generate) | After each chapter completed / 每完成一章 |

---

## §9. Output Format / 輸出格式

### Bilingual Format / 雙語格式

All report content in `report.md` MUST follow this structure:
`report.md` 的所有內容必須遵循以下結構：

```markdown
## {Chapter}.{Section} {English Title}
## {Chapter}.{Section} {中文標題}

{English paragraph with evidence tags [L1], [L2], etc. and source URLs}

{對應的中文段落，同樣的證據標注和來源 URL}
```

### Output Directory / 輸出目錄

```
outputs/{product-slug}/
├── checkpoint-0.md
├── sources.md
├── audit-urls.md
├── plan.md
├── audit-claims.md
├── report.md          ← The final report / 最終報告
├── audit-final.md
└── metadata.yaml      ← Snapshot metadata / 快照元資料
```

---

## §10. Completion / 完成流程

After Phase 3.5 completes successfully:
Phase 3.5 成功完成後：

1. Generate `metadata.yaml` with all required fields / 生成 metadata.yaml
2. Update `docs/index.md` library index / 更新圖書館索引
3. Git add, commit, and push all files / Git 加入、提交、推送所有檔案
4. Report completion summary to user / 向使用者報告完成摘要

```
🎉 Research complete! / 研究完成！

📊 Summary / 摘要:
- Product / 產品: {brand} {model}
- Quality grade / 品質評級: {A/B/C}
- Total sources / 來源總數: {N}
- L1 sources / L1 來源: {N}
- Word count / 字數: {N}
- Report: outputs/{slug}/report.md
- Online: https://stereosurfer.github.io/pro-article-generator/outputs/{slug}/
```

---

## §11. Phase Progress Reporting / 階段進度報告

During execution, report progress in this format:
執行過程中，以以下格式報告進度：

```
📍 Phase {X}: {Phase Name} / {中文名稱}
   ├── Loading: {file being loaded}
   ├── Executing: {current action}
   └── Status: {progress indicator}
```

On completion:
```
✅ Phase {X} complete / Phase {X} 完成
   ├── Output: {filename} ({lines} lines)
   ├── Key metric: {value}
   └── Next: Phase {X.X}
```
