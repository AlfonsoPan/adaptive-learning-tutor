---
name: study-motor-papers
description: "Automatic trigger gate: use this skill only when the current user message contains the exact contiguous Chinese phrase 分析论文. Do not trigger for synonyms, implied intent, attachments alone, or requests such as 读论文, 读文献, 翻译论文, 精读论文, 论文分析, 看一下这篇论文, or 分析文献 when 分析论文 is absent. After that exact phrase is present, translate and teach motor, motor-control, and power-electronics papers or technical literature from PDF, DOCX, images, URLs, or DOI references while preserving figures, tables, equations, captions, footnotes, appendices, and cross-references; assess prerequisite knowledge; derive key formulas; explain every figure; create durable study notes; and generate new instructional diagrams with the embedded interactive teaching SVG specification. Explicit $study-motor-papers invocation remains available."
---

# Study Motor Papers

## Invocation gate

- Before applying this workflow, confirm that the current user message literally contains the contiguous substring `分析论文`, or that the user explicitly invoked `$study-motor-papers`.
- If neither condition is true, do not apply this skill, do not load its references, and handle the request normally without starting the paper workflow.

## Objective

Turn one source paper into four coordinated outcomes:

1. Create a source-faithful Chinese translation that can be read independently.
2. Conduct one paper-wide, fundamentals-only pre-reading assessment, then generate the complete paragraph-by-paragraph study notes in one pass.
3. Add a careful interpretation beneath every figure without confusing inference with the paper's claims.
4. Create supplementary interactive teaching SVGs where a new diagram materially improves understanding, without replacing or altering the source figures.

Do not replace the requested full translation with a summary. Do not mix teaching commentary into the translation text itself; place commentary in clearly labeled blocks or in the separate study record.

## Load the relevant instructions

- Read [references/translation-qa.md](references/translation-qa.md) before inventorying, translating, reconstructing, or validating the source.
- Read [references/learning-loop.md](references/learning-loop.md) before starting paragraph analysis or asking knowledge-check questions.
- Read [references/figure-analysis.md](references/figure-analysis.md) before interpreting any figure, diagram, plot, or multi-panel Fig.
- Read [references/output-formats.md](references/output-formats.md) before creating the final study-note artifact or deciding between Obsidian Markdown and PDF.
- Before creating or reconstructing any teaching diagram, read [references/interactive-teaching-svg.md](references/interactive-teaching-svg.md) completely and use [assets/interactive-teaching-svg-template.svg](assets/interactive-teaching-svg-template.svg) as the mandatory skeleton.
- Read all five references when the user requests the complete workflow and instructional diagrams are warranted.

## Execute the workflow

### 1. Establish the source and scope

- Use the attached paper when provided. If the paper is absent, ask for the file, URL, DOI, or exact citation.
- Default to the entire paper, including appendices, notes, and references. Narrow the scope only when the user explicitly requests a chapter, page range, or figure.
- Detect scanned pages, unreadable formulas, missing pages, password protection, and low-resolution figures before translating.
- Inspect page images as well as extracted text. Never trust extraction alone for equations, columns, subscripts, superscripts, or figure placement.

### 2. Build a completeness inventory

- Record the source page count and enumerate headings, figures, tables, displayed equations, footnotes, appendices, and references.
- Preserve source paragraph boundaries after repairing line-wrap and multi-column extraction errors.
- Create a progress ledger for long papers. Mark every unit as `pending`, `translated`, `checked`, or `uncertain`.
- State any inaccessible or illegible item precisely. Never silently omit it.

### 3. Produce the Chinese master translation

- Translate precisely and completely, preserving document order, numbering, hierarchy, citations, units, symbols, and cross-references.
- Retain each original figure and equation. Translate captions, table text, and prose; add a Chinese key for English labels embedded in figures instead of destructively replacing the original image.
- Keep every newly generated teaching SVG supplementary and clearly labeled. Never substitute it for the original figure or present reconstructed geometry or curves as source evidence.
- Keep terminology consistent through a bilingual glossary. Prefer established Chinese motor-control terminology, and retain the English term on first occurrence when ambiguity is possible.
- Default to an editable DOCX plus a PDF reading copy when document tools are available. Otherwise create a structured Markdown deliverable with all extracted assets. Do not leave a long paper only as chat messages.
- Place a labeled `Fig X 图解` block immediately below every figure. Keep it visually separate from the translated caption.

### 4. Validate before teaching

- Compare the finished document against the inventory. Account for every page and every structured element.
- Verify all formulas, indices, signs, vectors, matrices, axis labels, legends, numbers, and units against the rendered source.
- Render and visually inspect the output. Fix clipped figures, broken equations, orphaned captions, unreadable tables, and misplaced commentary.
- Report uncertain OCR or translation choices in a short issue list. Claim completeness only after the ledger is closed.

### 5. Run one assessment and generate the study notes

- Begin after the master translation is complete unless the user explicitly requests chapter-by-chapter delivery.
- Process every source paragraph in order and identify it stably, such as `§3.2-P04`.
- First scan the entire paper and map each paragraph to the detailed prerequisite concepts needed to understand it. Deduplicate repeated concepts while retaining distinct sub-concepts.
- Build one paper-wide multiple-choice assessment covering all material prerequisite gaps. Test transferable knowledge the reader could reasonably know before reading. Never test equation numbers, figure results, experimental values, authors' claims, or other answers available only from the paper.
- Present all questions together in one neutral, tappable form with a single submission action when supported. If that is unavailable, present one numbered `A / B / C` answer sheet and ask the user to reply once with all selections.
- Wait for the complete answer submission. Do not reveal solutions or start paragraph analysis beforehand.
- Score the assessment once and generate the complete study record in one pass. For every paragraph, preserve this order:
  1. `原文`
  2. `对应中文`
  3. `基础知识补充` when the mapped concept was answered incorrectly, left blank, or marked unsure
  4. `段落分析`
  5. `结论边界`
- Insert each missing foundation at its first relevant paragraph, then use short callbacks instead of repeating the lesson verbatim in later paragraphs.
- Fully expand the key mathematical reasoning in the first affected analysis. Show coordinate transformations, scalar-axis equations, plant/observer subtraction, error dynamics, approximations, substitutions, and coefficient matching as applicable. Do not hide a material step behind phrases such as “substitution gives.”
- Do not run follow-up or recheck questions unless the user explicitly requests them or the submitted answers are unusable.
- When a spatial relationship, signal path, formula mechanism, or prerequisite concept benefits materially from a new diagram, create a single-file interactive teaching SVG under the study-note assets directory and link it to the exact paragraph, figure, or formula it explains.
- Determine the current client at study-note generation time and follow [references/output-formats.md](references/output-formats.md): create an Obsidian Markdown note set on desktop and a verified PDF on mobile. An explicit user format request overrides automatic detection.
- Save the resulting full study record as a durable artifact rather than flooding the chat with the entire paper.

### 6. Apply technical-review discipline

- Separate `原文直接给出`, `作者的解释/结论`, and `我的推断`.
- Independently check causal claims, assumptions, operating ranges, and contradictions. Do not agree with either the user or the paper automatically.
- Prefer formulas, data, figures, code, and cited evidence over plausible storytelling.
- Label confidence as high, medium, or low when interpretation is not directly established.
- Explicitly flag missing evidence, inconsistent notation, suspicious plots, or conclusions that exceed the presented data.

### 7. Maintain durable progress

- For work spanning multiple turns, resume from the ledger instead of restarting or re-translating completed sections.
- After the single assessment response, generate the study record with the question map, the user's answers, misconceptions corrected, and concepts demonstrated.
- At completion, deliver the validated Chinese translation and the platform-appropriate consolidated study record, plus a concise list of remaining uncertainties.

## Non-negotiable quality rules

- Never invent missing text, equations, citations, curves, colors, labels, or experimental conditions.
- Never infer a figure solely from its caption when the actual figure can be inspected.
- Never replace a source figure with a teaching SVG, and never put inferred data, curves, colors, labels, or geometry into a supplementary SVG without an explicit evidence label.
- Never simplify or paraphrase away qualifiers such as “approximately,” “under the assumption,” or “in the tested range.”
- Never expose the correct choice before the user answers, recommend an answer, or make the correct option conspicuously longer.
- Never use paper-specific conclusions as a proxy for prerequisite mastery in the pre-reading assessment.
- Never split the diagnostic into sequential question turns when the interface or message size can carry one complete assessment.
- Never call a partial translation “全文翻译.”
- Honor the user's request to skip, pause, revisit, or deepen any paragraph without losing the paper-wide progress state.
