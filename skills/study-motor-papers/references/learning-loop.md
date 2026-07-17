# One-shot paper learning workflow

## Contents

1. Paragraph mapping
2. Paper-wide prerequisite diagnosis
3. One-submission assessment
4. Answer evaluation
5. Full study-note generation
6. Mastery and traceability

## 1. Paragraph mapping

Analyze every source paragraph separately. Assign stable IDs derived from the section and paragraph order, such as `§2.3-P01`. Treat captions, equation-definition blocks, algorithms, and table notes as specialized units rather than silently skipping them. Handle figures through the figure-analysis reference.

Before writing questions, create an internal map:

| Paragraph ID | Argument role | Required concepts | Detail needed | Question IDs |
|---|---|---|---|---|
| §2.3-P01 | introduces observer error model | back-EMF, disturbance decomposition | distinguish signal from modeled disturbance | Q03, Q04 |

Group consecutive paragraphs only for understanding the argument. Preserve separate paragraph analysis in the final notes.

## 2. Paper-wide prerequisite diagnosis

Scan the entire translated paper before testing:

1. Identify every prerequisite whose absence would materially change or block understanding of a paragraph.
2. Break broad topics into the smallest useful distinctions. For example, do not test only “understands Bode plots” when the paper relies separately on corner-frequency slope, phase asymptote, and phase wrapping.
3. Deduplicate the same concept across paragraphs and map one question to all affected paragraphs.
4. Use more than one question for a concept only when different sub-skills are independently required.
5. Exclude mere terminology that the paper defines locally, historical facts, and arithmetic that does not illuminate the reasoning.
6. Convert each dependency into a context-neutral pre-reading question. A reader must be able to answer from prior fundamentals without having seen this paper.

Do not ask the reader to recall or infer this paper's equation numbers, block-diagram wiring, figure trends, table values, experimental settings, reported limits, or authors' conclusions. Those belong in the later paragraph analysis, not in the prerequisite diagnosis.

Likely motor-paper prerequisites include reference-frame transforms, electrical versus mechanical angular frequency, back-EMF formation, voltage/current models, integrator drift, frequency-response interpretation, observer convergence, cross-coupling, PLL behavior, inverter nonlinearity, sampling delay, coordinate and sign conventions, and evidence versus causal inference.

Do not impose a fixed question count. Cover all material details once, while keeping the assessment proportional to the paper.

## 3. One-submission assessment

### Question construction

- Use three plausible, mutually exclusive choices by default.
- Add `不确定/需要先复习` only when a fourth neutral choice is supported without displacing a meaningful distractor.
- Randomize correct-answer positions across the assessment.
- Keep choices similar in length, specificity, and grammatical form.
- Build distractors from realistic misconceptions.
- Test conceptual discrimination rather than rote definition whenever possible.
- State any sign convention or coordinate convention needed to make a fundamentals question unambiguous.
- Do not mark, recommend, bold, hint at, or stylistically distinguish the correct choice.
- Give each question a stable ID and map it back to the affected paragraphs.

### Preferred interactive form

When an inline interactive form capability is available:

- Render all questions in one accessible form.
- Use one radio-button group per question and one submit button for the entire assessment.
- Allow the user to review and change selections before submission.
- Show completion status, but do not show correctness, hints, or solutions.
- On submit, send only the question IDs and selected option IDs back to the conversation.
- Keep the answer key out of the client-side form and visible markup.
- Prevent accidental partial submission, or clearly treat blank questions as `不确定` after confirmation.

When such a form is unavailable, present one compact numbered answer sheet and ask for a single response such as `1B 2A 3C ...`. Do not split the questions across turns merely because a question-at-a-time UI exists. Split into labeled page sections within the same form or message only when layout requires it; retain one final submission.

After presenting the assessment, stop and wait. Do not reveal answers or generate the paragraph notes in that turn.

## 4. Answer evaluation

Evaluate the complete submission once:

- Mark each concept as `mastered`, `partial`, `gap`, or `unanswered` from direct evidence.
- Treat blanks and explicit uncertainty as gaps that need teaching, not as wrong reasoning.
- If a question is genuinely ambiguous, exclude it from diagnosis and explain the ambiguity in the final record.
- If the user selected a defensible interpretation not represented by the key, revise the key instead of forcing the intended answer.
- Do not ask recheck questions by default.

Create an internal remediation map:

| Concept | Result | First affected paragraph | Later paragraphs | Teaching depth |
|---|---|---|---|---|

## 5. Full study-note generation

Generate the entire study record after the one assessment submission. Start with a concise diagnostic overview, then process all paragraphs in source order. Apply the platform-specific packaging and note structure in [output-formats.md](output-formats.md).

Use this sequence for every paragraph:

### §x.x-Pyy

**原文**

> Exact source paragraph.

**对应中文**

> Faithful translated paragraph.

**基础知识补充** *(include when a mapped prerequisite is `gap`, `partial`, or `unanswered`)*

- start from physical intuition;
- give the minimum necessary definition and equation;
- use one boundary condition, counterexample, or limiting case;
- connect the concept directly to the sentence, equation, or figure about to be analyzed.

Teach a missing concept fully at its first relevant paragraph. At later paragraphs, refer back to that explanation and add only the new detail needed there.

**段落分析**

- explain the paragraph's role in the paper's argument;
- unpack difficult sentences and notation;
- show how the logic follows and which assumptions it needs;
- connect it to earlier equations, figures, or control blocks;
- state the practical implementation meaning when justified;
- identify contradictions or alternative explanations.

For a key formula chain, expand the mathematics at its first occurrence instead of only citing the final equation:

1. define the frame, sign convention, states, inputs, and error variables;
2. expand complex-vector equations into scalar d/q or α/β equations when that reveals the coupling terms;
3. write the plant and observer equations side by side, then subtract them term by term;
4. show the exact error dynamics before applying small-angle, steady-state, time-scale-separation, or parameter-matching assumptions;
5. write each approximation explicitly, including the discarded order or derivative;
6. expand determinants and characteristic polynomials, then match coefficients when pole placement is used;
7. carry signs, pole-pair factors, units, and electrical/mechanical speed conversions through the derivation;
8. state where the derivation ceases to be exact and what fails at zero speed, reversal, saturation, or parameter mismatch.

Use a complete derivation once and short equation callbacks later. Do not replace algebra with “similarly,” “after simplification,” or “substitution gives” when the omitted step controls the sign, gain, stability, or physical interpretation.

**结论边界**

- `原文直接给出` — explicitly stated or visible;
- `作者主张` — the authors' interpretation or conclusion;
- `我的推断` — additional reasoning with high/medium/low confidence;
- `仍缺证据` — what the paragraph cannot establish.

Do not add `基础知识补充` merely to lengthen a paragraph whose mapped concepts were demonstrated. Avoid generic restatement; resolve why the paragraph matters and what is easy to misunderstand.

End the record with:

- assessment result by concept, not a vanity score alone;
- corrected misconceptions and their paragraph locations;
- a terminology and notation glossary;
- links between key figures, equations, and conclusions;
- unresolved ambiguities or claims needing external evidence;
- optional topics for deeper follow-up, without automatically starting another quiz.

## 6. Mastery and traceability

Maintain this table in the study record:

| Concept | State | Evidence/question | Affected paragraphs | Where taught |
|---|---|---|---|---|

Update it only from submitted answers or explicit user statements. Do not infer mastery from job title alone.

Also retain:

- the complete question set and the user's selected answers;
- the paragraph-to-concept map;
- the answer-key rationale after submission;
- any ambiguous questions removed from evaluation;
- the completion state of all paragraph notes.

This traceability must make it possible to revise one diagnosis later without regenerating unrelated parts of the study notes.
