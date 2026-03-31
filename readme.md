# Pro Audio Report Generator

> 一套針對專業音頻設備與麥克風的「論文級產品研究報告」自動化產生系統。
> An automated system for generating academic-grade product research reports on professional audio equipment and microphones.

基於 **Perplexity Pro (Deep Research + Computer)** 運作，含多語系搜尋策略、證據分級、三層審計機制與成本控制規範。

Powered by **Perplexity Pro (Deep Research + Computer)**, featuring multilingual search strategies, evidence grading, a three-tier audit mechanism, and cost control standards.

---

## 目錄 / Table of Contents

- [系統概覽 / Overview](#系統概覽--overview)
- [Repo 結構 / Repository Structure](#repo-結構--repository-structure)
- [使用流程 / Workflow](#使用流程--workflow)
- [版本管理原則 / Versioning](#版本管理原則--versioning)
- [待補充檔案 / TODO](#待補充檔案--todo)

---

## 系統概覽 / Overview

本系統將一份音頻設備研究報告的產出流程拆解為 **6 個階段 + 3 層審計**，每個階段對應一份 prompt 檔案，確保輸出品質可追蹤、可重現。

This system decomposes the production of an audio equipment research report into **6 phases + 3 audit layers**, each corresponding to a dedicated prompt file, ensuring traceable and reproducible output quality.

---

## Repo 結構 / Repository Structure

```
pro-article-generator/
├── README.md                          # 本文件 / This file
├── spec/                              # 系統規格文件 / System specification docs
│   ├── report-template.md             # 報告章節架構模板 / Report chapter structure template
│   ├── source-strategy.md             # 搜尋與來源策略 / Search & source strategy
│   ├── evidence-levels.md             # 證據分級定義 / Evidence level definitions
│   └── audit-strategy.md              # 審計機制規範 / Audit mechanism spec  [TODO]
├── prompts/                           # 各階段提示詞 / Phase prompts
│   ├── space-instructions.md          # Perplexity Space 設定指令 / Space setup instructions
│   ├── phase1-search.md               # Phase 1: 多語系搜尋 / Multilingual search  [TODO]
│   ├── phase1-5-audit-url.md          # Phase 1.5: URL 審計 / URL audit  [TODO]
│   ├── phase2-plan.md                 # Phase 2: 報告規劃 / Report planning  [TODO]
│   ├── phase2-5-audit-claims.md       # Phase 2.5: 引用比對 / Claims audit  [TODO]
│   ├── phase3-generate.md             # Phase 3: 逐章生成 / Chapter generation  [TODO]
│   └── phase3-5-audit-final.md        # Phase 3.5: 數字一致性掃描 / Final audit  [TODO]
├── sources/                           # 可信來源清單 / Trusted source lists
│   ├── trusted-media.md               # 各語系可信媒體清單 / Trusted media by language  [TODO]
│   └── trusted-forums.md              # 各語系可信論壇清單 / Trusted forums by language  [TODO]
├── cost/                              # 成本控制 / Cost control
│   └── cost-control.md                # 成本估算與控制策略 / Cost estimation & strategy  [TODO]
└── outputs/                           # 報告輸出目錄 / Report output directory
    └── [product-name]/                # 每份報告一個資料夾 / One folder per report
        ├── sources.md
        ├── audit-urls.md
        ├── audit-claims.md
        ├── plan.md
        ├── report.md
        └── audit-final.md
```

> 標記 `[TODO]` 的檔案尚未建立，詳見[待補充檔案](#待補充檔案--todo)。
> Files marked `[TODO]` are not yet created. See [TODO section](#待補充檔案--todo).

---

## 使用流程 / Workflow

每次產生新報告，依序執行以下步驟：
Follow these steps in order to generate a new report:

| 步驟 / Step | 動作 / Action | 輸出 / Output |
|---|---|---|
| 1 | 在 Perplexity Space 設定 `space-instructions.md` | Space 就緒 |
| 2 | Deep Research → 貼入 `phase1-search.md`（替換設備名） | `sources.md` |
| 3 | 執行 `phase1-5-audit-url.md` | `audit-urls.md` |
| 4 | 貼入 `phase2-plan.md` | `plan.md` |
| 5 | 執行 `phase2-5-audit-claims.md` | `audit-claims.md` |
| 6 | 貼入 `phase3-generate.md`（逐章） | `report.md` |
| 7 | 執行 `phase3-5-audit-final.md` | `audit-final.md` |
| 8 | 將所有輸出存入 `outputs/[product-name]/` | 報告歸檔 |

---

## 版本管理原則 / Versioning

- **模板與提示詞更新**：在 `spec/` 與 `prompts/` 裡直接編輯，Git commit 留下紀錄。
  **Template & prompt updates**: Edit directly in `spec/` and `prompts/`; Git commit serves as the changelog.

- **已完成的報告**：`outputs/` 裡的內容不回頭修改；若需更新則建新版本資料夾（例：`neumann-u87ai-v2/`）。
  **Completed reports**: Never modify content inside `outputs/`; create a new versioned folder for updates (e.g., `neumann-u87ai-v2/`).

- **審計策略調整**：每次修改 `spec/audit-strategy.md` 時，必須在檔案內說明修改原因與日期。
  **Audit strategy changes**: Every modification to `spec/audit-strategy.md` must include the reason and date inside the file.

---

## 待補充檔案 / TODO

以下檔案已規劃但尚未建立，歡迎按優先序補充：
The following files are planned but not yet created:

### 高優先 / High Priority
- [ ] `spec/audit-strategy.md` — 三層審計的詳細執行規則
- [ ] `prompts/phase1-search.md` — 多語系搜尋階段提示詞
- [ ] `prompts/phase2-plan.md` — 報告規劃階段提示詞
- [ ] `prompts/phase3-generate.md` — 逐章生成階段提示詞

### 中優先 / Medium Priority
- [ ] `prompts/phase1-5-audit-url.md` — URL 審計提示詞
- [ ] `prompts/phase2-5-audit-claims.md` — 引用比對提示詞
- [ ] `prompts/phase3-5-audit-final.md` — 數字一致性掃描提示詞
- [ ] `cost/cost-control.md` — Token 成本估算與控制策略

### 低優先 / Low Priority
- [ ] `sources/trusted-media.md` — 各語系可信媒體清單
- [ ] `sources/trusted-forums.md` — 各語系可信論壇清單

---

## 規格文件快速索引 / Spec Quick Reference

| 檔案 / File | 說明 / Description |
|---|---|
| `spec/report-template.md` | 報告 8 章節固定架構 / Fixed 8-chapter report structure |
| `spec/source-strategy.md` | 4 輪搜尋流程與語言涵蓋要求 / 4-round search process & language coverage |
| `spec/evidence-levels.md` | Level 1–4 證據分級定義與引用規則 / Evidence levels 1–4 definitions & citation rules |
| `spec/audit-strategy.md` | 三層審計執行規範（待建） / Three-tier audit execution spec (TODO) |
| `prompts/space-instructions.md` | Perplexity Space 設定與 Agentic workflow 說明 / Space setup & agentic workflow |
