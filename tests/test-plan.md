# 🧪 Test Plan — Audio Researcher Antigravity Workflow

> 本文件定義 14 個模組的測試案例與驗收標準。
> This document defines test cases and acceptance criteria for all 14 modules.

詳見 implementation_plan.md 中的完整測試案例表。

## 測試原則 / Testing Principles

1. **模組 1-11**: 使用 `tests/mock-data/` 中的模擬資料進行格式與邏輯驗證
2. **模組 5+**: Phase 測試會實際執行但限制範圍（單輪搜尋、單章生成）
3. **模組 14**: 端對端完整測試（Shure SM58，真實搜尋）
4. **每個模組**: 遵循 `feat → test → fix → commit` 循環

## 測試結果存放位置

- `tests/test-results/NNN-module-name.md`
