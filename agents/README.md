# Agent Skills 架構說明 / Agent Skills Architecture

> 基於 Claude Code Agent Skills 標準規範  
> Based on Claude Code Agent Skills Standard

最後更新：2026-03-31

---

## 目錄 / Table of Contents

- [概述 / Overview](#概述--overview)
- [架構設計 / Architecture](#架構設計--architecture)
- [核心 Agents](#核心-agents)
- [支援 Skills](#支援-skills)
- [使用方式 / Usage](#使用方式--usage)
- [跨平台部署 / Cross-Platform Deployment](#跨平台部署--cross-platform-deployment)

---

## 概述 / Overview

本系統將音頻設備研究報告生成流程拆解為 **3 個核心 Agent** 和 **4 個可重用 Skill**，符合以下設計原則：

### 設計原則 / Design Principles

1. **模組化 / Modularity**  
   每個 Agent 專注單一職責，可獨立運作

2. **可組合性 / Composability**  
   Skills 可被多個 Agents 調用，避免重複

3. **平台無關 / Platform Agnostic**  
   遵循標準 prompt 格式，可在任何 LLM 平台使用

4. **可追蹤性 / Traceability**  
   每個階段輸出明確定義，便於審計

---

## 架構設計 / Architecture

```
┌─────────────────────────────────────────────────────┐
│                  Orchestration Layer                │
│          (User / Python Script / Workflow)          │
└──────────────────┬──────────────────────────────────┘
                   │
        ┌──────────┼──────────┐
        │          │          │
┌───────▼────┐ ┌──▼──────┐ ┌─▼────────┐
│ Research   │ │Planning │ │ Writing  │
│   Agent    │ │ Agent   │ │  Agent   │
└─────┬──────┘ └───┬─────┘ └────┬─────┘
      │            │             │
      └────────┬───┴─────┬───────┘
               │         │
        ┌──────▼─────────▼──────┐
        │   Shared Skills Pool  │
        ├───────────────────────┤
        │ • Evidence Grader     │
        │ • Cross-Ref Checker   │
        │ • Number Auditor      │
        │ • Multilingual Search │
        └───────────────────────┘
```

---

## 核心 Agents

### 1. Research Agent（研究專員）

**檔案**: `research-agent.md`

**職責**:  
- 執行多語系深度搜尋（EN/ZH-TW/ZH-CN/JA）
- URL 有效性驗證與分級
- 生成結構化來源清單

**對應階段**: Phase 1 + Phase 1.5  
**輸入**: 產品名稱、搜尋參數  
**輸出**: `sources.md`, `audit-urls.md`

**調用 Skills**:  
- Multilingual Search Skill
- Evidence Grader Skill

---

### 2. Planning Agent（規劃專員）

**檔案**: `planning-agent.md`

**職責**:  
- 分析來源內容，規劃報告結構
- 分配證據到各章節
- 執行聲明交叉驗證

**對應階段**: Phase 2 + Phase 2.5  
**輸入**: `sources.md`, `report-template.md`  
**輸出**: `plan.md`, `audit-claims.md`

**調用 Skills**:  
- Evidence Grader Skill
- Cross-Reference Checker Skill

---

### 3. Writing Agent（寫作專員）

**檔案**: `writing-agent.md`

**職責**:  
- 按照計畫逐章生成報告
- 確保學術風格與一致性
- 執行最終數字審計

**對應階段**: Phase 3 + Phase 3.5  
**輸入**: `plan.md`, `sources.md`  
**輸出**: `report.md`, `audit-final.md`

**調用 Skills**:  
- Number Consistency Auditor Skill
- Cross-Reference Checker Skill

---

## 支援 Skills

### 1. Evidence Grader Skill

**檔案**: `skills/evidence-grader.md`

判斷來源的證據等級（Level 1-4），基於：
- 來源類型（官網 > 評測 > 論壇）
- 內容完整度
- 可驗證性

---

### 2. Cross-Reference Checker Skill

**檔案**: `skills/cross-reference-checker.md`

比對多個來源的聲明一致性：
- 識別矛盾
- 計算共識度
- 標註需要進一步驗證的項目

---

### 3. Number Consistency Auditor Skill

**檔案**: `skills/number-auditor.md`

掃描全文規格數字：
- 檢查單位一致性
- 識別不一致的數值
- 生成審計報告

---

### 4. Multilingual Search Skill

**檔案**: `skills/multilingual-search.md`

執行語言特定搜尋策略：
- 構建語言專屬查詢
- 針對性平台選擇
- 結果結構化輸出

---

## 使用方式 / Usage

### 快速開始 / Quick Start

1. **選擇執行模式**：
   - 手動模式：逐步複製貼上 Agent prompts
   - 自動模式：使用 Python orchestrator（見 `examples/`）

2. **準備輸入**：
   ```
   產品名稱: "Neumann U87 Ai"
   目標語言: ["en", "zh-tw", "zh-cn", "ja"]
   ```

3. **執行流程**：
   ```
   Research Agent → sources.md + audit-urls.md
         ↓
   Planning Agent → plan.md + audit-claims.md
         ↓
   Writing Agent → report.md + audit-final.md
   ```

### 詳細範例 / Detailed Examples

參見 `examples/` 資料夾：
- `manual-workflow.md` - 手動執行完整流程
- `api-orchestration.py` - Python API 自動化腳本
- `claude-projects.md` - 在 Claude Projects 中設置

---

## 跨平台部署 / Cross-Platform Deployment

### 支援平台 / Supported Platforms

| 平台 | 使用方式 | 備註 |
|------|---------|------|
| Claude (Anthropic) | 直接貼上 Agent prompts | 原生支援 Agent 模式 |
| ChatGPT (OpenAI) | 使用 Custom GPTs | 需手動設置 instructions |
| Gemini (Google) | 貼上 prompts | 完整功能支援 |
| Perplexity Pro | 使用 Deep Research + Computer | 搜尋能力最強 |
| Local LLMs | 透過 API 調用 | 需自行實作 orchestration |

### 平台特定配置 / Platform-Specific Config

詳見 `examples/platform-configs/` 資料夾

---

## 檔案結構 / File Structure

```
agents/
├── README.md                    # 本文件 / This file
├── research-agent.md            # 研究專員 Agent
├── planning-agent.md            # 規劃專員 Agent
├── writing-agent.md             # 寫作專員 Agent
├── skills/                      # 可重用技能
│   ├── evidence-grader.md
│   ├── cross-reference-checker.md
│   ├── number-auditor.md
│   └── multilingual-search.md
└── examples/                    # 使用範例
    ├── manual-workflow.md
    ├── api-orchestration.py
    ├── claude-projects.md
    └── platform-configs/
        ├── claude.md
        ├── chatgpt.md
        ├── gemini.md
        └── perplexity.md
```

---

## 版本管理 / Versioning

- Agent prompts 更新時，在檔案內註記版本號與更新日期
- 保持向後相容性，重大變更時建立新版本檔案
- 參考主 repo 的版本管理原則

---

## 貢獻指南 / Contributing

歡迎提出改進建議：
1. 新增 Skills 時，請遵循現有格式
2. Agent 更新需同步更新本 README
3. 提供使用範例到 `examples/` 資料夾

---

## 授權 / License

與主 repository 相同授權條款
