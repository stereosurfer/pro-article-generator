---
description: 研究任何產品並生成論文級研究報告。輸入產品名稱即可全自動執行。Research any product and generate an academic-grade research report.
---

# Research Workflow / 研究工作流

When the user asks to research a product (e.g., "幫我研究 Neumann U87Ai", "Research the Shure SM58"), follow these steps:

1. Read the SKILL.md file for complete instructions:
   ```
   view_file _agents/skills/researcher/SKILL.md
   ```

2. Follow SKILL.md from §2 (Product Identification) onwards. The SKILL.md contains ALL rules for:
   - Product identification and user confirmation (§2)
   - Checkpoint chain enforcement (§3)
   - Phase execution instructions (§4)
   - Context budget management (§5)
   - Crash recovery (§6)
   - Backtrack rules (§7)
   - Incremental saves (§8)

3. Phase instruction files are located at:
   ```
   _agents/skills/researcher/phases/phase-{N}-{name}.md
   ```

4. All output goes to:
   ```
   outputs/{product-slug}/
   ```

// turbo-all
