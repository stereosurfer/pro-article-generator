# Pro Audio Report Generator

> 一套針對專業音頻設備與麥克風的「論文級產品研究報告」自動化產生系統。
> An automated system for generating academic-grade product research reports on professional audio equipment, optimized for Perplexity Pro.

本系統基於 **Perplexity Pro (Deep Research + Computer)** 運作，整合了多語系搜尋策略、證據分級（L1-L4）、三層自動化審計與 **3-Agent 協同工作流**。

---

## 目錄 / Table of Contents

- [系統概覽 / Overview](#系統概覽--overview)
- [Repo 結構 / Repository Structure](#repo-結構--repository-structure)
- [Agent 技能架構 / Agent Skills](#agent-技能架構--agent-skills)
- [核心技能 / Core Skills](#核心技能--core-skills)
- [使用流程 / Workflow](#使用流程--workflow)
- [快速索引 / Quick Reference](#快速索引--quick-reference)
- [Antigravity 集成 / Integration](#antigravity-集成--integration)

---

## 系統概覽 / Overview

本系統將研究報告的產出流程拆解為 **7 個執行階段**（對齊 `spec/workflow-v1.1.md`），由 **Research**, **Planning**, 與 **Writing** 三大代理人協作完成。其核心目標是確保報告的「事實準確性」與「技術深度」。

---

## Repo 結構 / Repository Structure

```text
pro-article-generator/
├── spec/                # 系統規格文件 (Specs)
│   ├── workflow-v1.1.md    # 7個執行階段規範 (核心)
│   ├── report-template.md  # 報告 9 章節架構模板
│   ├── source-strategy.md  # 4 輪搜尋策略
│   ├── evidence-levels.md  # 證據分級 (L1-L4) 定義
│   └── audit-strategy.md   # 三層審計執行規範
├── agents/              # 代理人規格
│   ├── research-agent.md   # P0-P1.5 (搜尋與核網)
│   ├── planning-agent.md   # P2-P2.5 (規劃與審計)
│   ├── writing-agent.md    # P3-P3.5 (生成與終審)
│   └── skills/             # 自動化技能 (Skills)
│       ├── url-auditor.md           # 來源可信度審計
│       ├── evidence-grader.md        # 證據分級評分
│       ├── cross-reference-checker.md # 跨來源事實比對
│       ├── number-auditor.md         # 規格數字精確度審計
│       ├── outline-builder.md        # 結構映射生成
│       └── claims-auditor.md         # 最終聲明一致性核查
├── prompts/             # 實作提示詞 (Phase-based Prompts)
├── sources/             # 信任來源清單 (Trusted Media/Forums)
└── outputs/             # 報告輸出歸檔
```

---

## Agent 技能架構 / Agent Skills

1. **Research Agent**: 專注於多語系（英/日/中）資訊採集，負責 P0-P1.5 階段，過濾不可信來源。
2. **Planning Agent**: 負責 P2-P2.5 階段，將原始資料轉化為結構化大綱，執行證據分級審計。
3. **Writing Agent**: 負責 P3-P3.5 階段，執行專業潤稿、術語檢查與最終一致性審計。

---

## 核心技能 / Core Skills

- **URL Auditor**: 自動分析網域權威性（Media vs Forum vs Store）。
- **Evidence Grader**: 根據規格文件將證據分為 L1 (官方) 到 L4 (傳聞)。
- **Number Auditor**: 嚴格比對技術參數（如 靈敏度、阻抗、頻響曲線）。
- **Cross-Reference Checker**: 確保不同來源對同一事實的描述無衝突。

---

## 使用流程 / Workflow

| 階段 | 動作 | 負責 Agent/Skill |
|:---:|:---|:---|
| **P0-P1** | 初始化與多語系搜尋 | Research Agent |
| **P1.5** | **URL 審計** | `url-auditor` |
| **P2** | 大綱規劃與來源映射 | Planning Agent |
| **P2.5** | **引用比對與分級** | `evidence-grader`, `cross-reference-checker` |
| **P3** | 專業內容逐章生成 | Writing Agent |
| **P3.5** | **最終一致性審計** | `number-auditor`, `claims-auditor` |

---

## 快速索引 / Quick Reference

- **流程規範**: `spec/workflow-v1.1.md`
- **證據標準**: `spec/evidence-levels.md`
- **Agent 詳解**: `agents/README.md`

---

## Antigravity 集成 / Integration

本 Repo 的 Agent 與 Skill 規格完全相容於 **Google Antigravity** 環境：
1. **複製 Specs**: 將 `agents/` 下的 `.md` 文件導入 Antigravity 代理人指令。
2. **載入技能**: 在 Antigravity 的「自定義技能」中關聯 `agents/skills/` 的邏輯。
3. **執行**: 依照 `prompts/` 內的指令順序執行對應的 Phase。
