# Pro Audio Report Generator

一套針對專業音頻設備與麥克風的「論文級產品研究報告」自動化產生系統。
基於 Perplexity Pro (Deep Research + Computer) 運作，含多語系搜尋策略、
證據分級、三層審計機制與成本控制規範。

## Repo 結構

pro-audio-report-generator/
├── README.md
├── spec/
│   ├── report-template.md       # 章節架構模板
│   ├── source-strategy.md       # 搜尋與來源策略
│   ├── evidence-levels.md       # 證據分級定義
│   └── audit-strategy.md        # 審計機制規範
├── prompts/
│   ├── space-instructions.md    # Space 設定指令
│   ├── phase1-search.md         # 搜尋階段提示詞
│   ├── phase1-5-audit-url.md    # URL 審計提示詞
│   ├── phase2-plan.md           # 計畫階段提示詞
│   ├── phase2-5-audit-claims.md # 引用比對提示詞
│   ├── phase3-generate.md       # 逐章生成提示詞
│   └── phase3-5-audit-final.md  # 數字一致性掃描提示詞
├── sources/
│   ├── trusted-media.md         # 各語系可信媒體清單
│   └── trusted-forums.md        # 各語系可信論壇清單
├── cost/
│   └── cost-control.md          # 成本估算與控制策略
└── outputs/
    └── [product-name]/
        ├── sources.md
        ├── audit-urls.md
        ├── audit-claims.md
        ├── plan.md
        ├── report.md
        └── audit-final.md

## 使用流程（每次產新報告）

1. 在 Perplexity Space 確認 space-instructions.md 已設定
2. 開新 Thread → Deep Research → 貼入 phase1-search.md（換設備名）
3. 取得來源清單後 → 執行 phase1-5-audit-url.md
4. 審計通過 → 貼入 phase2-plan.md
5. 確認計畫 → 執行 phase2-5-audit-claims.md
6. 審計通過 → 貼入 phase3-generate.md（逐章）
7. 報告完成 → 執行 phase3-5-audit-final.md
8. 將所有輸出存入 outputs/[product-name]/

## 版本管理原則

- 模板與提示詞更新：在 spec/ 與 prompts/ 裡直接編輯，Git commit 留下紀錄
- 已完成的報告：outputs/ 裡的內容不回頭修改，若需更新則建新版本資料夾
  （例如：neumann-u87ai-v2/）
- 每次對審計策略的調整，必須在 audit-strategy.md 裡說明修改原因與日期