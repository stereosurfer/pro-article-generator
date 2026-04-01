# Phase 0: Initialization / 初始化

> Phase 0 of 7 — Research Workflow v2.0

---

## Prerequisites / 前置條件

- **Required input**: Product name (confirmed by user via SKILL.md §2)
- **Required input**: Category slug (confirmed by user)
- **No checkpoint file required** (this is the first phase)

---

## Output / 產出

- **File**: `outputs/{slug}/checkpoint-0.md`
- **Minimum lines**: 15

---

## Task Instructions / 任務指令

### Step 1: Create output directory / 建立輸出目錄

Create the directory `outputs/{slug}/` if it does not exist.
Slug format: lowercase, hyphens instead of spaces. Example: "Neumann U87 Ai" → `neumann-u87-ai`
若目錄不存在，建立 `outputs/{slug}/`。

### Step 2: Load and verify standards / 載入並驗證標準文件

Load these 3 files and confirm they exist and are non-empty:
載入以下 3 份文件，確認存在且非空：

1. `_agents/skills/researcher/standards/evidence-levels.md`
2. `_agents/skills/researcher/standards/report-structure.md`
3. `_agents/skills/researcher/standards/audit-rules.md`

For each file, record:
- File name / 檔案名稱
- First heading line (proves you actually read it) / 第一行標題（證明你確實讀了）
- Approximate line count / 大約行數

### Step 3: Load category configuration / 載入品類設定

Load `categories/{category}/category.md` and record:
載入 `categories/{category}/category.md` 並記錄：

- Category name / 品類名稱
- Applicable product types / 適用產品類型
- Search language priority / 搜尋語系優先順序
- Chapter customizations summary / 章節調整摘要

### Step 4: Record product details / 記錄產品詳情

Record the confirmed product information:
記錄已確認的產品資訊：

- Full product name (brand + model) / 完整產品名稱
- Category / 品類
- Variant/era notes (if any) / 變體/年代備註
- Research focus / 研究重點
- Origin language (for search priority) / 原產地語言

### Step 5: Write checkpoint-0.md / 寫入 checkpoint-0.md

Write all the above information to `outputs/{slug}/checkpoint-0.md` with the mandatory footer format:
將以上所有資訊寫入 `outputs/{slug}/checkpoint-0.md`，包含強制尾部格式。

---

## Output Template / 輸出模板

```markdown
# Phase 0: Initialization Complete / 初始化完成

## Standards Verified / 已驗證標準文件
1. ✅ evidence-levels.md — "{first heading}" ({N} lines)
2. ✅ report-structure.md — "{first heading}" ({N} lines)
3. ✅ audit-rules.md — "{first heading}" ({N} lines)

## Category Loaded / 已載入品類
- Category: {category_slug}
- Product types: {list}
- Languages: {priority list}
- Chapter adjustments: {summary}

## Product Confirmed / 已確認產品
- Product: {brand} {model}
- Category: {category}
- Variant: {variant or "standard"}
- Origin language: {language}
- Research focus: {focus}

---
## 📊 Phase 0 Statistics / Phase 0 統計
- Specs confirmed / 已確認規格: 3/3
- Category loaded / 已載入品類: {category}
- Product confirmed / 已確認產品: {brand} {model}
- Phase start time / 開始時間: {ISO 8601}
- Phase end time / 結束時間: {ISO 8601}
- Next phase / 下一步: Phase 1 (Multilingual Search / 多語系搜尋)
- Resume instruction / 恢復指令: Skip Phase 0, proceed to Phase 1 / 跳過 Phase 0，直接進入 Phase 1
```

---

## Success Signal / 成功訊號

```
✅ Phase 0 complete / Phase 0 完成
   ├── Output: checkpoint-0.md ({N} lines)
   ├── Standards: 3/3 verified
   └── Next: Phase 1 (Search)
```

## Failure Handling / 失敗處理

- If any standard file is missing → report error, ask user to check repository / 標準文件缺失 → 報告錯誤
- If category directory is missing → ask user to specify category or create one / 品類目錄缺失 → 請使用者指定或建立
