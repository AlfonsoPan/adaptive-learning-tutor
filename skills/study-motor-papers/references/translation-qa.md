# Translation preservation and QA

## Contents

1. Source inventory
2. Paragraph and terminology rules
3. Equations and symbols
4. Figures and tables
5. Citations and peripheral content
6. OCR and difficult sources
7. Completeness and visual QA
8. Deliverable structure

## 1. Source inventory

Before translating, build a ledger like this:

| ID | Source location | Kind | Identifier/title | Status | Uncertainty |
|---|---|---|---|---|---|
| S01 | pp. 1–2 | section | Introduction | pending | none |
| F03 | p. 5 | figure | Fig. 3(a–c) | pending | panel c labels small |
| E12 | p. 6 | equation | (12) | pending | minus sign needs visual check |

Inventory at minimum:

- total pages and page-size/orientation changes;
- title, authors, affiliations, abstract, keywords, headings, and acknowledgements;
- every normal paragraph in reading order;
- figures and all subpanels;
- tables, displayed equations, algorithm blocks, and code fragments;
- footnotes, endnotes, appendices, nomenclature, and references.

For two-column papers, reconstruct reading order from layout. Treat a displayed equation and its immediately dependent prose as distinct ledger items while preserving their adjacency.

## 2. Paragraph and terminology rules

- Translate meaning, logical relation, modality, and technical qualifiers rather than mirroring English word order.
- Do not merge or split source paragraphs in the master translation unless layout reconstruction requires it. Record any necessary split or merge.
- Preserve negation, comparison direction, conditional clauses, scope words, and confidence language.
- Retain the English term in parentheses at first occurrence when the Chinese term is ambiguous or has multiple industry usages.
- Build a paper-local glossary for repeated terms. Prefer the paper's own notation and definitions over generic conventions.
- Check potentially confusing motor-control pairs explicitly, such as mechanical/electrical speed, phase/line quantity, peak/RMS value, rotor/stator frame, saliency/non-saliency, flux/flux linkage, and disturbance/noise.
- Keep acronyms unchanged after introducing their full Chinese and English names.

Do not “repair” an author's apparent technical error inside the translated prose. Translate faithfully, then flag the suspected error in a separate note.

## 3. Equations and symbols

- Reproduce equations exactly rather than translating mathematical symbols.
- Verify every sign, fraction, exponent, derivative, integration limit, transpose, inverse, complex conjugate, vector arrow/boldface, subscript, superscript, and equation number.
- Preserve whether a variable is scalar, vector, matrix, phasor, or complex quantity.
- Translate `where` clauses and symbol definitions completely.
- Do not normalize symbols to familiar conventions if the paper uses a different convention.
- Check formula references in prose after pagination or reconstruction.
- If OCR confidence is low, insert the equation as a high-resolution source crop and mark it for manual verification instead of guessing.

Create a notation table when the paper uses many variables:

| Symbol | Paper definition | Units | First location | Notes |
|---|---|---|---|---|

## 4. Figures and tables

- Retain the original image at readable resolution and preserve its figure number and panel lettering.
- Translate the official caption faithfully. Keep it separate from the added interpretation.
- For text embedded in the original image, add a compact bilingual label table below the caption. Do not erase traces, axes, or annotations by drawing over them.
- Verify axis quantity, unit, scale type, sign direction, legend, color, line style, markers, annotations, operating point, and sampling window.
- Translate every table header, row label, note, and footnote while preserving numeric values, units, significant digits, and emphasis.
- Rebuild tables as real tables when practical; use a high-resolution crop only if reconstruction would risk changing the content.

## 5. Citations and peripheral content

- Preserve citation numbering and author-year references exactly.
- Retain bibliographic fields, DOIs, URLs, patent numbers, and standard numbers in their original form.
- Keep reference titles in the source language by default; an optional Chinese title may follow in brackets without replacing the original.
- Translate appendices, author notes, acknowledgements, conflict statements, and data-availability statements unless the user excludes them.

## 6. OCR and difficult sources

- Detect whether each page contains selectable text or only an image.
- Render scanned pages at sufficient resolution before OCR, deskew when necessary, and preserve a page-to-text mapping.
- Compare OCR against the page image for formulas, Greek letters, subscripts, column boundaries, and hyphenated line endings.
- Mark illegible content as `[原文不清：页码/区域]`; do not fill gaps from context.
- When a newer source version or supplementary file is required, tell the user exactly what is missing.

## 7. Completeness and visual QA

Perform these checks before declaring completion:

1. Compare source and output section order.
2. Reconcile counts for figures, panels, tables, displayed equations, footnotes, appendices, and references.
3. Check all equation images or typeset equations against source renderings.
4. Check every figure caption and in-text figure reference.
5. Search for untranslated running prose and accidental omissions.
6. Search for broken glyphs, replacement characters, and OCR artifacts.
7. Render the deliverable page by page and inspect clipping, overlap, blank pages, typography, caption placement, and image legibility.
8. Record every unresolved item with its exact location and severity.

Use a final reconciliation table:

| Element | Source count | Output count | Verified | Notes |
|---|---:|---:|---|---|
| Pages/sections |  |  |  |  |
| Figures/panels |  |  |  |  |
| Tables |  |  |  |  |
| Displayed equations |  |  |  |  |
| Footnotes/appendices |  |  |  |  |
| References |  |  |  |  |

## 8. Deliverable structure

Default to two durable deliverables:

1. `论文标题_中文保真译本.docx` plus a rendered PDF reading copy.
2. A platform-appropriate study record generated in one pass after the paper-wide assessment is submitted. Follow [output-formats.md](output-formats.md): Obsidian Markdown on desktop and PDF on mobile.

The translation should follow this structure:

- translated title and original title;
- authors and bibliographic information;
- translation notes and terminology policy;
- full translated body in source order;
- each original figure/table/equation in its corresponding position;
- translated caption and embedded-label key;
- `Fig X 图解` after each figure;
- bilingual terminology and notation glossary;
- completeness reconciliation and unresolved-item list.

The master translation must remain readable when all added `Fig X 图解` blocks are ignored.
