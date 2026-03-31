# URL Auditor Skill / URL 稽核技能

基於 Workflow v1.1 Phase 1.5 的 URL 有效性與相關性驗證技能。
Skill specification for URL validity and relevance verification based on Workflow v1.1 Phase 1.5.

---

## 功能描述 / Description

**URL Auditor** 負責對搜尋結果中的 URL 進行深度稽核，確保 Research Agent 產出的來源清單具有高品質與真實性。

**URL Auditor** is responsible for deep auditing of URLs in search results to ensure high quality and authenticity.

---

## 稽核標準 / Audit Standards

| 標準 / Standard | 說明 / Description | 權重 |
|----------------|-------------------|------|
| **Reachability** | URL 是否可正常訪問 (HTTP 200) | 必備 |
| **Relevance** | 內容是否確實提及目標產品 | 40% |
| **Recency** | 發表日期是否在近 2 年內 | 20% |
| **Authority** | 來源網站是否具備專業度 | 40% |

---

## 輸入參數 / Input Parameters

```json
{
  "urls": ["https://...", "https://..."],
  "target_product": "Neumann TLM 103",
  "min_relevance_score": 0.7
}
```

---

## 輸出結果 / Output Results

```json
{
  "summary": {
    "total": 10,
    "valid": 8,
    "rejected": 2
  },
  "results": [
    {
      "url": "https://...",
      "status": "valid",
      "relevance_score": 0.95,
      "reason": "Expert review with technical measurements"
    }
  ]
}
```

---

## 與流程整合 / Workflow Integration

- 被 **Research Agent** 在 Phase 1.5 呼叫。
- 若 `valid` 數量低於 20，觸發自動回溯至 Phase 1。
