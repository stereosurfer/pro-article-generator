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

本系統將音頻設備研究報告生成流程拆解為 **2 個核心 Agent** 和 **4 個專屬 Skill**，對齊 `spec/workflow-v1.1.md` 的 7 個執行階段。

### 設計原則 / Design Principles

1. **模組化 / Modularity**: 每個 Agent 專注特定階段，可獨立運作。
2. **可組合性 / Composability**: Skills 可被多個 Agents 調用。
3. **平台無關 / Platform Agnostic**: 遵循標準 Prompt 格式。
4. **可追蹤性 / Traceability**: 每個階段輸出明確定義，便於審計。

---

## 架構設計 / Architecture

```text
┌─────────────────────────────────────────────────────┐
│                 Orchestration Layer                 │
│          (User / Python Script / Workflow)          │
└──────────────────┬──────────────────────────────────┘
                   │
         ┌─────────┴─────────┐
         │                   │
   ┌─────▼──────┐      ┌─────▼──────┐
   │  Research  │      │  Writing   │
   │   Agent    │      │   Agent    │
   └─────┬──────┘      └─────┬──────┘
         │                   │
         └─────────┬─────────┘
                   │
   ┌───────────────▼───────────────┐
   │       Shared Skills Pool      │
   ├───────────────────────────────┤
   │ • url-auditor.md              │
   │ • evidence-grader.md          │
   │ • outline-builder.md          │
   │ • claims-auditor.md           │
   └───────────────────────────────┘
```

---

## 核心 Agents

### 1. Research Agent（研究專員）
**檔案**: `research-agent.md`
**職責**: 執行 Phase 0-1.5，包含初始化、多語系搜尋與 URL 稽核。
**調用 Skills**: `url-auditor.md`, `evidence-grader.md`

### 2. Writing Agent（寫作專員）
**檔案**: `writing-agent.md`
**職責**: 負責 Phase 2-3.5，包含大綱規劃、引用稽核、內容生成與最終一致性掃描。
**調用 Skills**: `outline-builder.md`, `claims-auditor.md`

---

## 支援 Skills

### 1. URL Auditor
**檔案**: `skills/url-auditor.md`
**功能**: 稽核網址有效性與存活狀態 (Phase 1.5)。

### 2. Evidence Grader
**檔案**: `skills/evidence-grader.md`
**功能**: 判定證據等級 (L1-L4) 並過濾低品質內容。

### 3. Outline Builder
**檔案**: `skills/outline-builder.md`
**功能**: 自動對齊 9 章節架構並進行來源映射 (Phase 2)。

### 4. Claims Auditor
**檔案**: `skills/claims-auditor.md`
**功能**: 交叉驗證事實主張與原始來源的吻合度 (Phase 2.5)。

---

## 使用方式 / Usage

1. **執行 Research**: 獲取產品關鍵字，產出 `sources.md`。
2. **審核 URL**: 透過 `url-auditor` 確認來源可靠。
3. **規劃計畫**: 使用 `outline-builder` 產出 `plan.md`。
4. **生成內容**: 由 Writing Agent 逐章產出報告，並由 `claims-auditor` 核實。

---

## 檔案結構 / File Structure

```text
agents/
├── README.md           # 本文件
├── research-agent.md   # Phase 0-1.5
├── writing-agent.md    # Phase 2-3.5
└── skills/             # 自動化技能
    ├── url-auditor.md
    ├── evidence-grader.md
    ├── outline-builder.md
    └── claims-auditor.md
```
