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

本系統將音頻設備研究報告生成流程拆解為 **3 個核心 Agent** 和 **6 個專屬 Skill**，對齊 `spec/workflow-v1.1.md` 的 7 個執行階段。

### 設計原則 / Design Principles

1. **模組化 / Modularity**: 每個 Agent 專注特定階段，可獨立運作。
2. **可組合性 / Composability**: Skills 可被多個 Agents 調用。
3. **平台無關 / Platform Agnostic**: 遵循標準 Prompt 格式，相容於 Google Antigravity。
4. **可追蹤性 / Traceability**: 每個階段輸出明確定義，便於審計。

---

## 架構設計 / Architecture

```text
┌─────────────────────────────────────────────────────┐
│                Orchestration Layer                  │
│        (User / Python Script / Workflow)            │
└──────────────────┬──────────────────────────────────┘
                   │
    ┌──────────────┴──────────────┬──────────────┐
    │                             │              │
┌───▼──────────┐         ┌────────▼──────┐ ┌─────▼──────┐
│   Research   │         │   Planning    │ │   Writing   │
│    Agent     │         │    Agent      │ │    Agent    │
└───┬──────────┘         └────────┬──────┘ └─────┬──────┘
    │                             │              │
    └──────────────┬──────────────┴──────────────┘
                   │
    ┌──────────────▼──────────────┐
    │      Shared Skills Pool     │
    ├─────────────────────────────┤
    │ • url-auditor.md            │
    │ • evidence-grader.md        │
    │ • cross-reference-checker.md│
    │ • number-auditor.md         │
    │ • outline-builder.md        │
    │ • claims-auditor.md         │
    └─────────────────────────────┘
```

---

## 核心 Agents

### 1. Research Agent（研究專員）
- **檔案**: `research-agent.md`
- **職責**: 執行 Phase 0-1.5，包含初始化、多語系搜尋與 URL 稽核。
- **調用 Skills**: `url-auditor.md`

### 2. Planning Agent（規劃專員）
- **檔案**: `planning-agent.md`
- **職責**: 執行 Phase 2-2.5，負責大綱生成、證據分級與事實比對。
- **調用 Skills**: `outline-builder.md`, `evidence-grader.md`, `cross-reference-checker.md`

### 3. Writing Agent（寫作專員）
- **檔案**: `writing-agent.md`
- **職責**: 負責 Phase 3-3.5，包含內容潤稿、數字核查與最終一致性審計。
- **調用 Skills**: `number-auditor.md`, `claims-auditor.md`

---

## 支援 Skills

### 1. URL Auditor
- **檔案**: `skills/url-auditor.md`
- **功能**: 稽核網域權威性與來源可靠度.

### 2. Evidence Grader
- **檔案**: `skills/evidence-grader.md`
- **功能**: 根據規格判定證據等級 (L1-L4)。

### 3. Cross-Reference Checker
- **檔案**: `skills/cross-reference-checker.md`
- **功能**: 比對不同來源對同一事實的描述.

### 4. Number Auditor
- **檔案**: `skills/number-auditor.md`
- **功能**: 核對技術參數中的數字準確性.

### 5. Outline Builder
- **檔案**: `skills/outline-builder.md`
- **功能**: 自動生成對齊 9 章節架構的大綱.

### 6. Claims Auditor
- **檔案**: `skills/claims-auditor.md`
- **功能**: 交叉驗證最終聲明與原始來源.

---

## 使用方式 / Usage

1. **執行 Research**: 產出 `sources.md`。
2. **執行 Planning**: 進行大綱規劃與證據分級，產出 `plan.md`。
3. **執行 Writing**: 生成報告並執行最終審計。

---

## 檔案結構 / File Structure

```text
agents/
├── README.md           # 本文件
├── research-agent.md   # Phase 0-1.5
├── planning-agent.md   # Phase 2-2.5
├── writing-agent.md    # Phase 3-3.5
└── skills/             # 自動化技能
    ├── url-auditor.md
    ├── evidence-grader.md
    ├── cross-reference-checker.md
    ├── number-auditor.md
    ├── outline-builder.md
    └── claims-auditor.md
```
