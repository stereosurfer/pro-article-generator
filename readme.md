# Pro Audio Report Generator

> 一套針對專業音頻設備與麥克風的「論文級產品研究報告」自動化產生系統。
> An automated system for generating academic-grade product research reports on professional audio equipment and microphones.

基於 **Perplexity Pro (Deep Research + Computer)** 運作，整合了多語系搜尋策略、證據分級（L1-L4）、三層自動化審計與 Agentic Workflow 技能架構。

---

## 目錄 / Table of Contents

- [系統概覽 / Overview](#系統概覽--overview)
- [Repo 結構 / Repository Structure](#repo-結構--repository-structure)
- [Agent 技能架構 / Agent Skills](#agent-技能架構--agent-skills)
- [使用流程 / Workflow](#使用流程--workflow)
- [待補充檔案 / TODO](#待補充檔案--todo)

---

## 系統概覽 / Overview

本系統將研究報告的產出流程拆解為 **7 個執行階段**（對齊 `spec/workflow-v1.1.md`），並透過兩大核心代理人（Research & Writing Agent）與多項專屬技能（Skills）協作完成。

---

## Repo 結構 / Repository Structure

```text
pro-article-generator/
├── spec/                # 系統規格文件 (Specs)
│   ├── workflow-v1.1.md    # 7個執行階段規範 (核心)
│   ├── report-template.md  # 報告 8 章節架構模板
│   ├── source-strategy.md  # 4 輪搜尋策略
│   ├── evidence-levels.md  # 證據分級 (L1-L4) 定義
│   └── audit-strategy.md   # 三層審計執行規範
├── agents/              # 代理人規格 (Agent Specs)
│   ├── research-agent.md   # 負責 Phase 0-1.5 (搜尋與核網)
│   ├── writing-agent.md    # 負責 Phase 2-3.5 (規劃與生成)
│   └── skills/             # 自動化技能 (Skills)
│       ├── url-auditor.md     # 網址有效性稽核
│       ├── evidence-grader.md # 證據等級自動分級
│       ├── outline-builder.md # 章節大綱自動對齊
│       └── claims-auditor.md  # 引用與主張比對
├── prompts/             # 實作提示詞 (Prompts) [TODO]
├── sources/             # 可信來源資料庫 [TODO]
└── outputs/             # 報告輸出歸檔
```

---

## Agent 技能架構 / Agent Skills

本系統採模組化設計，兩大代理人分工如下：

1.  **Research Agent**: 負責初始化（Phase 0）、多語系搜尋（Phase 1）與 URL 稽核（Phase 1.5）。
2.  **Writing Agent**: 負責大綱規劃（Phase 2）、引用稽核（Phase 2.5）、章節生成（Phase 3）與最終掃描（Phase 3.5）。

---

## 使用流程 / Workflow

| 階段 | 動作 | 核心輸出 | 負責 Agent/Skill |
|------|------|----------|-----------------|
| **P0-P1** | 初始化與多語系搜尋 | `sources.md` | Research Agent |
| **P1.5** | **URL 審計** | `audit-urls.md` | `url-auditor` |
| **P2** | 大綱規劃與來源映射 | `plan.md` | `outline-builder` |
| **P2.5** | **引用比對審計** | `audit-claims.md` | `claims-auditor` |
| **P3** | 專業內容逐章生成 | `report.md` | Writing Agent |
| **P3.5** | **最終一致性審計** | `audit-final.md` | Writing Agent |

---

## 待補充檔案 / TODO

- [ ] `prompts/` 內的詳細提示詞實作
- [ ] `sources/trusted-media.md` 各語系媒體清單
- [ ] `cost/cost-control.md` Token 成本管理策略

---

## 快速索引 / Quick Reference

- **最新流程規範**: [spec/workflow-v1.1.md](spec/workflow-v1.1.md)
- **證據分級標準**: [spec/evidence-levels.md](spec/evidence-levels.md)
- **Agent 架構說明**: [agents/README.md](agents/README.md)
