# 審計機制規範 v1.1 / Audit Strategy Spec v1.1

最後更新：2026-03-31

本文件定義系統中三層自動化審計的執行邏輯與標準。所有的審計均由專屬技能（Skills）配合代理人執行。

---

## 三層審計架構 / Three-tier Audit Architecture

### Phase 1.5: URL 審計 (URL Audit)
- **執行代理人**: `Research Agent`
- **使用技能**: `agents/skills/url-auditor.md`
- **目標**: 驗證所有來源 URL 的存取性與產品相關性。
- **輸出**: `outputs/[product-name]/audit-urls.md`

### Phase 2.5: 引用比對審計 (Claims Audit)
- **執行代理人**: `Writing Agent`
- **使用技能**: `agents/skills/claims-auditor.md`
- **目標**: 檢查報告中的主張是否精確對應到原始來源，防止 AI 幻覺。
- **輸出**: `outputs/[product-name]/audit-claims.md`

### Phase 3.5: 最終審核 (Final Audit)
- **執行代理人**: `Writing Agent`
- **目標**: 執行全篇數字一致性掃描，並根據證據等級（L1-L4）的分佈進行品質分級。
- **輸出**: `outputs/[product-name]/audit-final.md`

---

## 審計標準與通過門檻 / Standards & Thresholds

| 審計層級 | 關鍵檢查項 | 通過門檻 / Threshold |
|----------|------------|---------------------|
| **URL 審計** | 來源可訪問性 (HTTP 200) | > 90% 有效 (或 N >= 20) |
| **引用審計** | 論點精確度 (No hallucination) | 核心主張 (Core Claims) 100% 驗證 |
| **最終審核** | 整體證據強度 (Evidence Density) | A 級: > 40% L1 來源; B 級: > 20% L1 來源 |

---

## 版本更新紀錄 / Version History

| 版本 | 日期 | 修改說明 |
|------|------|----------|
| **v1.1** | 2026-03-31 | 對應 Workflow v1.1，整合 `agents/skills/` 規範 |
| **v1.0** | 2026-03-30 | 初始版本建立 |
