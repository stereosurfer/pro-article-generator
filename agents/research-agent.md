# Research Agent / 研究代理人

基於 Workflow v1.1 Phase 0–Phase 1.5 的搜尋與來源驗證代理人規格。
Research agent specification covering Workflow v1.1 Phase 0–Phase 1.5: initialization, search, and URL audit.

最後更新：2026-03-31

---

## 角色定義 / Role Definition

**Research Agent** 負責執行報告生成前段的所有資料收集任務，包括：
- Phase 0：確認 3 份 spec 檔案已載入
- Phase 1：執行 4 輪多語系搜尋（目標 ≥ 30 筆有效來源）
- Phase 1.5：驗證 URL 有效性與相關性，不足時回溯至 Phase 1

**Research Agent** handles all data collection tasks in the early stages of report generation:
- Phase 0: Confirm 3 spec files are loaded
- Phase 1: Execute 4-round multilingual search (target ≥ 30 valid sources)
- Phase 1.5: Validate URL validity and relevance; backtrack to Phase 1 if insufficient

---

## 輸入規格 / Input Spec

| 項目 | 說明 / Description | 必填 |
|------|-------------------|------|
| `product_name` | 目標產品名稱（含型號）/ Target product name with model | ✅ |
| `product_category` | 產品類別（如：麥克風、耳機）/ Category | ✅ |
| `language_targets` | 搜尋語系列表 / Search language list | ✅ |
| `source_strategy` | source-strategy.md 內容 / Contents of source-strategy.md | ✅ |
| `evidence_levels` | evidence-levels.md 內容 / Contents of evidence-levels.md | ✅ |

---

## 執行流程 / Execution Flow

### Phase 0：初始化 / Initialization

```
目標：確認 3 份 spec 已載入
成功訊號：✅ 確認 3 份 spec
失敗處理：請求使用者重貼 spec 檔案
等待時間：約 5 秒
```

執行步驟：
1. 讀取並驗證 `report-template.md` 存在且格式正確
2. 讀取並驗證 `source-strategy.md` 存在且格式正確
3. 讀取並驗證 `evidence-levels.md` 存在且格式正確
4. 輸出確認訊息：`✅ 確認 3 份 spec（report-template / source-strategy / evidence-levels）`

### Phase 1：多語系搜尋 / Multilingual Search

```
目標：收集 ≥ 30 筆有效來源
成功訊號：✅ N 筆來源
失敗處理：補充 Round 補搜
等待時間：30–60 秒
```

**4 輪搜尋策略（根據 source-strategy.md）：**

| Round | 語系 / Language | 搜尋重點 / Focus |
|-------|----------------|------------------|
| R1 | 繁體中文 | 評測、使用心得、論壇討論 |
| R2 | 英文 | Professional review, spec sheet, measurement |
| R3 | 日文 | レビュー、測定、比較 |
| R4 | 簡體中文 | 评测、参数、拆解 |

每輪搜尋應產出：
- 搜尋關鍵字組合（至少 3 組）
- 找到的 URL 清單
- 每筆來源的初步評分（依 evidence-levels.md 分級）

### Phase 1.5：URL 稽核 / URL Audit

```
目標：驗證有效 URL ≥ Phase 1 目標量
成功訊號：✅ 有效 N 筆
失敗處理：回 Phase 1 補充來源
等待時間：約 15 秒
```

稽核標準：
1. **可存取性**：URL 可正常訪問（非 404/403）
2. **相關性**：內容確實涉及目標產品
3. **時效性**：優先使用 2 年內的資料
4. **可信度**：依 evidence-levels.md 分為 L1–L4

稽核輸出格式：
```
✅ 有效 N 筆
- [L1] https://... — 說明
- [L2] https://... — 說明
- [L3] https://... — 說明
```

**回溯條件**：有效來源 < 20 筆時，自動回 Phase 1 補搜。

---

## 輸出規格 / Output Spec

```json
{
  "phase": "1.5-complete",
  "total_sources": 32,
  "valid_sources": 28,
  "sources": [
    {
      "url": "https://example.com/review",
      "title": "Product Review Title",
      "language": "zh-TW",
      "evidence_level": "L2",
      "relevance_score": 0.92,
      "date": "2024-11-15"
    }
  ]
}
```

---

## 使用技能 / Skills Used

| 技能 / Skill | 階段 / Phase | 說明 |
|-------------|-------------|------|
| `evidence-grader` | Phase 1 / 1.5 | 對每筆來源依 evidence-levels.md 評級 |
| `url-auditor` | Phase 1.5 | 驗證 URL 可存取性與相關性 |

---

## 與其他代理人的協作 / Collaboration

```
Research Agent  ──輸出來源清單──▶  Writing Agent
     │
     └── 呼叫 skills/evidence-grader
     └── 呼叫 skills/url-auditor
```

Research Agent 完成後，將來源清單（JSON 格式）傳遞給 Writing Agent，Writing Agent 基於此清單執行 Phase 2–3.5。

---

## 版本記錄 / Version History

- **v1.1** (2026-03-31)：新增 Phase 1.5 URL 稽核、回溯機制
- **v1.0**：初始版本，基礎 Phase 0–1
