# Workflow v1.1 專利生成流程階段表 / Workflow Phases

此檔案定義報告生成的 **7 個執行階段**，每階段包含預估等待時間、成功結束訊號與失敗處理方式。

This file defines the **7 execution phases** for report generation. Each phase includes estimated wait time, success signal, and failure handling.

---

## 階段表 / Phase Table

| Phase | 等待時間 / Wait Time | 結束訊號 / End Signal | 失敗處理 / Failure Handling |
|-------|---------|------------|----------------|
| **Phase 0** 初始化 / Init | 5秒 / 5s | ✅ 確認 3 份 spec | 重貼 spec 檔案 |
| **Phase 1** 搜尋 / Search | 30–60秒 / 30-60s | ✅ N 筆來源 | 補 Round 補搜 |
| **Phase 1.5** URL 稽核 / URL Audit | 15秒 / 15s | ✅ 有效 N 筆 | 回 Phase 1 |
| **Phase 2** 大綱 / Outline | 20秒 / 20s | ✅ 8 章就緒 | 補映射 |
| **Phase 2.5** Claims 稽核 / Claims Audit | 15秒 / 15s | ✅ VERIFIED 數 | 自動往下 |
| **Phase 3** 生成 / Generate | 60–120秒 / 60-120s | ✅ N 字報告 | 補章節 |
| **Phase 3.5** 最終審核 / Final Audit | 20秒 / 20s | ✅ 品質評級 | 補強建議 |

---

## 流程說明 / Workflow Description

### 總執行時間 / Total Execution Time
整體流程從初始化（確認 3 份 spec）到最終審核（品質評級）共需約 **2.5–4 分鐘**完成一份完整報告。

The entire workflow takes approximately **2.5-4 minutes** from initialization (confirming 3 specs) to final audit (quality rating) to complete one full report.

### 回溯機制 / Backtrack Mechanism

Phase 1.5 的 URL 稽核是**唯一會觸發回溯（回 Phase 1）的階段**，確保來源品質。

Phase 1.5 URL audit is the **only phase that triggers backtracking (back to Phase 1)** to ensure source quality.

---

## 階段詳細說明 / Phase Details

### Phase 0: 初始化 / Initialization
- **目的**: 確認 3 份 spec 檔案（report-template.md, source-strategy.md, evidence-levels.md）已載入
- **成功訊號**: "✅ 確認 3 份 spec"
- **失敗處理**: 重新貼上 spec 檔案

### Phase 1: 搜尋 / Search
- **目的**: 根據 source-strategy.md 執行 4 輪多語系搜尋
- **成功訊號**: "✅ N 筆來源" (N ≥ 30)
- **失敗處理**: 補充 Round 補搜

### Phase 1.5: URL 稽核 / URL Audit
- **目的**: 驗證來源 URL 有效性與相關性
- **成功訊號**: "✅ 有效 N 筆"
- **失敗處理**: 回到 Phase 1 補充來源

### Phase 2: 大綱 / Outline
- **目的**: 根據 report-template.md 生成 8 章大綱
- **成功訊號**: "✅ 8 章就緒"
- **失敗處理**: 補充章節映射

### Phase 2.5: Claims 稽核 / Claims Audit
- **目的**: 驗證引用與來源對應關係
- **成功訊號**: "✅ VERIFIED 數"
- **失敗處理**: 自動繼續（記錄警告）

### Phase 3: 生成 / Generate
- **目的**: 逐章生成完整報告內容
- **成功訊號**: "✅ N 字報告" (N ≥ 5000)
- **失敗處理**: 補充章節內容

### Phase 3.5: 最終審核 / Final Audit
- **目的**: 數字一致性掃描、品質評級
- **成功訊號**: "✅ 品質評級: [A/B/C]"
- **失敗處理**: 提供補強建議

---

## 使用說明 / Usage Instructions

1. **執行前**: 確保 3 份 spec 檔案已上傳至 Space
2. **執行中**: 根據階段訊號判斷進度
3. **失敗時**: 按照失敗處理欄位執行對應動作
4. **完成後**: 將輸出儲存至 `outputs/[product-name]/`

---

## 版本記錄 / Version History

- **v1.1** (2026-03-31): 新增 Phase 1.5 與 Phase 2.5 審核階段
- **v1.0**: 初始版本，基礎 5 個階段
