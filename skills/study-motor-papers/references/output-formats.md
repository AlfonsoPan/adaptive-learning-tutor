# Platform-specific study-note output

## Contents

1. Platform selection
2. Shared content model
3. Desktop: Obsidian Markdown
4. Mobile: verified PDF
5. Delivery and quality checks

## 1. Platform selection

Choose the study-note format at final note-generation time:

- Treat the macOS, Windows, or Linux desktop app and a desktop browser as `desktop`.
- Treat the native iOS or Android app and a mobile browser as `mobile`.
- Use reliable current client metadata or an explicit user statement. Do not rely on a device used in an earlier conversation.
- If the current client is unknown, ask one short format question before generating the artifact.
- Let an explicit request for Markdown, Obsidian, PDF, or another format override automatic selection.

This branch controls the **study-note artifact**. Continue to produce the complete Chinese translation and its PDF reading copy under the translation workflow on either platform.

## 2. Shared content model

Keep the intellectual content equivalent across desktop and mobile. Include:

1. paper metadata and evidence state;
2. a learning map showing the order in which ideas depend on one another;
3. assessment overview and concept-level mastery profile;
4. core problem and method structure;
5. key formulas and assumptions;
6. experimental or simulation platform;
7. full paragraph-by-paragraph study notes;
8. every `Fig X 图解` block;
9. main conclusions, possible counterexamples, and limitations;
10. mapping to motor-control code or implementation where justified;
11. reproducible experiments;
12. terminology, notation, and citations.

Use the evidence ladder consistently:

| Level | Meaning |
|---|---|
| A | reproduced on hardware |
| B | reproduced in simulation |
| C | independently derived |
| D | understood from the paper but not verified |
| E | unresolved or not verified |

Do not raise a claim's level merely because the explanation sounds convincing.

## 3. Desktop: Obsidian Markdown

### Package structure

Create a portable note folder:

```text
paper-slug/
├── paper-slug_精读笔记.md
├── concepts/
│   └── missing-concept.md
└── assets/
    └── fig-01.png
```

Create companion concept notes only for substantial gaps diagnosed by the assessment or for reusable concepts central to the paper. Keep incidental explanations inside the main paper note.

Use relative Obsidian embeds and wiki links:

```markdown
![[assets/fig-01.png]]
详见：[[concepts/反电势与电压模型]]
```

Do not require third-party Obsidian plugins or custom CSS.

### YAML frontmatter

Start the main paper note with:

```yaml
---
title: ""
authors: []
year:
journal: ""
doi: ""
tags:
  - motor-control
  - paper-study
collection: foc_control
status: reading
rating:
evidence_level: D
source_language: en
---
```

Choose one primary collection from `control_theory`, `electric_drive`, `motor_body`, `power_electronics`, `foc_control`, or `stm32_motor_engineering`. Choose additional domain tags from the paper rather than adding every possible tag. Use status values consistently: `unread`, `reading`, `derived`, `simulated`, `implemented`, or `verified`.

### Main note outline

Use this order:

```markdown
# 论文标题

## 学习地图
## 测验结果与能力画像
## 核心问题
## 方法结构
## 关键公式
## 假设条件
## 实验平台
## 逐段精读
## Fig 汇总与图解索引
## 主要结论
## 可能的反例与局限
## 对当前代码的映射
## 可复现实验
## 术语与符号
## 引用
```

- Add a compact Mermaid diagram under `学习地图` or `方法结构` only when dependency order, signal flow, or state transitions materially benefit from it.
- Use Obsidian-compatible KaTeX display blocks for equations: `$$ ... $$`.
- Use Markdown tables for notation, parameter comparisons, assessment results, and evidence levels.
- Use callouts sparingly for warnings, engineering implications, and unresolved claims.
- Keep original and translated paragraphs adjacent inside `逐段精读` as required by the learning workflow.

### Assessment answers

After the user submits the assessment, preserve each question, the selected answer, the correct reasoning, and the affected paragraphs. Put detailed answer reasoning in a native HTML fold:

```markdown
### Q03 · 反电势与扰动的区别

你的选择：B  
结果：需要补充

<details>
<summary>查看答案与推导</summary>

答案、物理直觉、必要公式、反例及相关段落。

</details>
```

Do not hide essential remediation only in the fold; repeat the necessary foundation at the first affected paragraph.

### Companion concept-note structure

Use short, RAG-friendly concept notes:

```markdown
# 概念名称

## 概念
## 公式
## 物理意义
## 工程影响
## 代码变量
## 常见问题
## 关联论文与段落
```

Keep each concept note focused on one concept. Link it back to the main paper note and the exact paragraph IDs.

## 4. Mobile: verified PDF

Create `论文标题_精读学习笔记.pdf` after the assessment. Use the same content model as the desktop note, but optimize for continuous mobile reading:

- use a single-column portrait layout;
- embed Chinese fonts and all figures;
- include a clickable table of contents and PDF bookmarks;
- use clear heading hierarchy, page numbers, and paragraph IDs;
- keep body text readable without mandatory horizontal panning;
- place formulas on separate lines and break derivations at logical steps;
- scale plots so legends, axes, and annotations remain legible;
- place exceptionally wide tables or block diagrams on a landscape page rather than shrinking them into illegibility;
- keep each figure with its translated caption and `Fig X 图解` block when practical;
- place the assessment overview before the paragraph notes and the detailed answer rationale in an appendix or clearly labeled section;
- retain evidence levels, counterexamples, code mapping, experiments, glossary, and citations.

Do not use Markdown-only conventions such as unresolved wiki links in the PDF. Convert every internal reference into a PDF bookmark, page reference, or clickable internal link.

Render every PDF page to images and inspect the result. Fix clipped formulas, missing glyphs, overlapping labels, blank pages, tiny legends, and broken links before delivery.

## 5. Delivery and quality checks

### Desktop checks

- Verify YAML frontmatter parses cleanly.
- Verify all Obsidian embeds use relative paths and every target asset exists.
- Verify wiki links resolve within the delivered folder.
- Verify Mermaid fences, KaTeX blocks, Markdown tables, and HTML folds are balanced.
- Keep filenames filesystem-safe and stable.

### Mobile checks

- Verify page count, bookmarks, clickable TOC, embedded fonts, and searchable Chinese text.
- Compare figure and equation counts to the source inventory.
- Inspect every rendered page at phone-like width as well as full-page view.

Deliver only the branch selected for the current client unless the user explicitly requests both. If a user continues the same study on another platform later, regenerate from the existing learning record rather than re-running the assessment.
