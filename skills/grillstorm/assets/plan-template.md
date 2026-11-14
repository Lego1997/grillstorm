<!--
Notes for the planning session. Delete this block from the finished plan.

- Keep the section numbers and headings. The initialization prompt and the evaluator brief refer to them.
- Write every path relative to the folder that holds this file.
- If there is no benchmark, remove the two passages in section 7 marked (benchmark only), and use the no-benchmark wording given in sections 4b, 5 and 7.
- Where there is a benchmark, delete the (benchmark only) markers and keep the text.
- Delete the bracketed no-benchmark instructions either way.
-->

# Plan: [deliverable title]

Agreed on [date]. Sections 3, 4 and 5 can be changed only by the human; every change is recorded in section 9. All paths are relative to the folder that holds this file.

## 1. Goal and context

- Deliverable: [what it is, in one line]
- Reader: [who reads it, and what they already know]
- What the reader does with it: [the decision or action it supports]
- Why now: [occasion, deadline]
- Position: [the recommendation or main finding the user has already settled on, or "the worker proposes it; the human reviews it at the round 1 pause"]
- Out of scope: [what this deliverable will not cover]

## 2. Spec and inputs

- Format and file: [for example, a Markdown file at `drafts/brief.md`]
- Length: [a limit the evaluator can count, such as a word count]
- Language and register: [for example, English, plain and direct]
- Inputs the worker must draw on:
  - [path or link, and what it is for]
- Other sources: [the worker may find its own, each linked where it is used | listed inputs only]
- Facts must not be invented: [figures, quotations, citations and so on]. A fact that is not in the inputs or in a source the reader can open is flagged in the draft as missing, not filled in. Proposals the deliverable itself makes, such as dates or targets, are allowed and must read as proposals.
- After the loop: [what the human still does, for example fill flagged gaps or convert the file format]

## 3. Structure

Bullets and sub-bullets only. Each bullet names an element and says what it has to do.

- [Section or element]: [its job]
  - [What goes inside]
    - [Detail, where the worker would otherwise have to guess]
- [Section or element]: [its job]
  - [What goes inside]

## 4. Success criteria

### 4a. Binary checks

Each check is true or false of the draft. The evaluator quotes the passage that proves its verdict.

- **C1. [Short name].** [Statement that is observably true or false of the draft.]
  - Check: [how the evaluator checks it]
  - Origin: [reference | user | user change | suggested add | research]
- **C2. [Short name].** [Statement.]
  - Check: [how]
  - Origin: [origin]

### 4b. Benchmark comparison

The evaluator reads the draft next to the benchmark named in section 5. The draft must win or tie on every dimension. The benchmark may be about a different topic; each dimension is about craft, not subject matter.

- **D1. [Dimension].** [What "stronger" means on this dimension.]
- **D2. [Dimension].** [What "stronger" means.]

[With no benchmark, replace everything under this heading with: "No benchmark was available. The loop runs on the binary checks alone."]

## 5. Benchmark and references

- Benchmark for comparison: [path], [why the user rates it]
- What to emulate: [the specific qualities agreed with the user]
- What not to copy: [content, dated material, things the user would change today]
- Other references: [path or link, and what each is for]
- Do not use: [anything in the workspace the worker should ignore, and why]

[With no benchmark, the first line reads "Benchmark for comparison: none", and "What to emulate" holds the standards agreed from research, with their sources.]

## 6. Loop protocol

- Roles
  - Worker: the session that drafts and revises.
  - Evaluator: a fresh sub-agent started for each round. It receives the brief in section 7 and nothing else from the worker's conversation: no reasoning, no earlier evaluation reports.
  - Human: owns sections 3, 4 and 5.
- Each round
  - The worker writes or revises the draft at [draft path].
  - The worker starts a fresh evaluator with the section 7 brief, word for word.
  - The worker saves the evaluator's report to [eval dir]/round-N.md.
  - The worker revises to fix everything the report marks as failed or lost.
- Human pause after round 1
  - The worker stops and shows the draft and the round 1 report.
  - The human confirms that the evaluator judged the right things, and that the position the draft takes is one they stand behind.
  - The human may amend the criteria or settle the position. Changes go in section 9.
  - After that the loop runs without check-ins.
- Stop when
  - the evaluator's result line says DONE, or
  - round 5 has been evaluated.
- At the stop, the worker reports
  - the final result line from the last evaluation
  - any checks still failing, and why they resisted
  - every gap it flagged in the draft that the human still has to fill
  - any change to the criteria it would propose. It proposes; it does not edit.
- If the tool cannot start sub-agents
  - After each draft the worker stops and hands the human the section 7 brief to run in a separate, fresh session. The human pastes the report back.

## 7. Evaluator brief

Give this to the evaluator word for word.

> You are an independent evaluator. You did not write this draft and you have no stake in it passing.
>
> Read sections 1 to 5 of the plan at [plan path]. Read the draft at [draft path]. (benchmark only) Read the benchmark at [benchmark path]. To verify claims you may open the inputs listed in section 2 and, if you have web access, the sources the draft links to.
>
> **Binary checks (section 4a).** Evaluate every check, every round, including ones that probably passed before. For each, give:
> - the verdict: PASS or FAIL
> - the evidence: a direct quote from the draft, with its location, that proves the verdict. For a check about something being absent, quote an instance to prove FAIL, or state what you searched for to prove PASS.
> - for a FAIL, one line on what is wrong. Do not rewrite the passage.
>
> If you cannot find evidence that a check passes, the verdict is FAIL. If a check needs something you cannot reach, such as a web link, the verdict is FAIL with the note "cannot verify", and you list what a human would need to open.
>
> (benchmark only) **Benchmark comparison (section 4b).** For each dimension, read both documents and say which is stronger: DRAFT, BENCHMARK or TIE. Support the call with one quote from each. The benchmark may be about a different topic; judge the craft the dimension names.
>
> **Result.** End with one line in this form:
> `CHECKS: [passed]/[total] · COMPARISON: [wins] wins, [ties] ties, [losses] losses · RESULT: DONE` or `REVISE`
>
> The result is DONE only if every check passes and there are no losses.
>
> Do not edit the draft. Do not grade generously: a human audits your first report against their own reading.

[With no benchmark, the result line is `CHECKS: [passed]/[total] · RESULT: DONE` or `REVISE`, and the sentence after it reads "The result is DONE only if every check passes."]

## 8. Assumptions, deferred decisions and open questions

- Assumptions: [what the planning session assumed without asking]
- Deferred decisions: [what the user was asked and left to the planning session's recommendation. The round 1 pause is the moment to revisit these.]
- Open questions: [what is still unknown, and who resolves it]

## 9. Change log

- [date]: plan agreed.
