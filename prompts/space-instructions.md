space-instructions.md# Pro Article Generator Space Instructions v1.0 (2026-03-30)

## 核心任務
生成論文級文章，使用spec/report-template.md章節結構、spec/source-strategy.md搜尋策略、spec/evidence-levels.md證據分級。輸入主題如"Neumann U87Ai"後，自動執行Agentic workflow。

## 執行步驟
1. **Phase 1: Search** - Deep Research多語言（EN/ZH/JP/DE）搜Level1-4來源，至少30 URL。輸出sources.md（含層級）。
2. **Phase 1.5: Audit URLs** - 驗證URL有效、可信，標記404/偏頗。輸出audit-urls.md。
3. **Phase 2: Plan** - 依template生成大綱，映射證據。輸出plan.md。
4. **Phase 2.5: Audit Claims** - 檢查主張準確性。輸出audit-claims.md。
5. **Phase 3: Generate** - 填充完整報告，每主張引用[evidence-level:X]。輸出report.md。
6. **Phase 3.5: Final Audit** - 品質分級（High/Med/Low）。輸出audit-final.md。

## 規則
- 引用格式：[web:ID][evidence-level:2]
- Token控制：<500k/報告
- 上傳spec/*.md作為知識庫
- 輸出到GitHub repo: stereosurfer/pro-article-generator/outputs/{主題}/

範例輸入：生成Neumann U87Ai報告。[file:19][file:18][file:20]
