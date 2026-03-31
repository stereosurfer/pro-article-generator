# Audit Rules v2.0 / 審計規則
# Universal standard — category-independent / 通用標準 — 與品類無關

> Last updated / 最後更新: 2026-03-31
> Derived from / 來源: spec/audit-strategy.md v1.1

---

## Three-Tier Audit Architecture / 三層審計架構

### Tier 1: URL Audit (Phase 1.5)

- **Trigger / 觸發時機**: After Phase 1 search completes / Phase 1 搜尋完成後
- **Target / 目標**: Verify all source URLs for accessibility and product relevance / 驗證所有來源 URL 的存取性與產品相關性
- **Output file / 輸出檔案**: `audit-urls.md`

**Pass threshold / 通過門檻:**

| Check / 檢查項 | Threshold / 門檻 |
|---|---|
| URL accessibility (HTTP 200) / URL 可訪問性 | > 90% valid OR ≥ 20 valid sources / 有效率 > 90% 或有效數 ≥ 20 |

**Backtrack rule / 回溯規則:**
- Valid sources < 20 → MUST return to Phase 1 for supplementary search / 有效來源 < 20 → 必須回 Phase 1 補搜

---

### Tier 2: Claims Audit (Phase 2.5)

- **Trigger / 觸發時機**: After Phase 2 outline completes / Phase 2 大綱完成後
- **Target / 目標**: Verify that report claims accurately correspond to original sources. Prevent AI hallucination. / 檢查報告主張是否精確對應原始來源，防止 AI 幻覺
- **Output file / 輸出檔案**: `audit-claims.md`

**Pass threshold / 通過門檻:**

| Check / 檢查項 | Threshold / 門檻 |
|---|---|
| Core claim accuracy (no hallucination) / 核心主張精確度 | 100% of core claims verified / 核心主張 100% 驗證 |
| Overall verification rate / 整體驗證率 | ≥ 70% verified / 已驗證 ≥ 70% |

**Backtrack rule / 回溯規則:**
- UNVERIFIED claims > 30% → Return to Phase 1 for supplementary search OR flag for human review / 未驗證 > 30% → 回 Phase 1 補搜或標記需人工確認

---

### Tier 3: Final Audit (Phase 3.5)

- **Trigger / 觸發時機**: After Phase 3 report generation completes / Phase 3 報告生成完成後
- **Target / 目標**: Number consistency scan + overall quality grading based on evidence level distribution / 全篇數字一致性掃描 + 依據證據等級分佈進行品質分級
- **Output file / 輸出檔案**: `audit-final.md`

**Quality grading / 品質分級:**

| Grade / 等級 | Criteria / 標準 |
|---|---|
| **A** | > 40% L1 sources, no number conflicts, ≥ 70% claims verified / L1 > 40%，無數字衝突，驗證率 ≥ 70% |
| **B** | > 20% L1 sources, ≤ 2 number conflicts (resolved), ≥ 70% claims verified / L1 > 20%，數字衝突 ≤ 2（已解決） |
| **C** | Below B criteria — flag for human review / 低於 B 標準 — 標記需人工審閱 |

---

## Checkpoint Chain Enforcement / 文件依賴鏈強制規則

Every phase MUST produce its designated output file. The next phase MUST read the previous phase's output file before starting. If the file does not exist or is empty, the phase MUST NOT proceed.

每個 Phase 必須產出其指定的輸出檔案。下一個 Phase 開始前必須讀取上一個 Phase 的輸出檔案。若檔案不存在或為空，該 Phase 不得執行。

| Current Phase / 當前 Phase | Must read first / 必須先讀取 | Must produce / 必須產出 |
|---|---|---|
| Phase 0 | (none) | checkpoint-0.md |
| Phase 1 | checkpoint-0.md | sources.md |
| Phase 1.5 | sources.md | audit-urls.md |
| Phase 2 | audit-urls.md | plan.md |
| Phase 2.5 | plan.md | audit-claims.md |
| Phase 3 | audit-claims.md | report.md |
| Phase 3.5 | report.md | audit-final.md + metadata.yaml |

---

## Mandatory File Footer / 強制文件尾部格式

Every checkpoint file MUST end with a statistics block in this exact format:

每份交接文件結尾必須包含以下格式的統計區塊：

```markdown
---
## 📊 Phase X Statistics / Phase X 統計
- [metric 1]: value
- [metric 2]: value
- Phase start time / 開始時間: ISO 8601
- Phase end time / 結束時間: ISO 8601
- Next phase / 下一步: Phase X.X (description)
- Resume instruction / 恢復指令: [how to resume from this point]
```
