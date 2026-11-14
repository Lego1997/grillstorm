# Plan: [deliverable title]

Agreed on [date] between [user] and the planning session. Sections 3, 4 and 5 can be changed only by the human; every change is recorded in section 9.

## 1. Goal and context

- Deliverable: [what it is, in one line]
- Reader: [who reads it, and what they already know]
- What the reader does with it: [the decision or action it supports]
- Why now: [occasion, deadline]
- Out of scope: [what this deliverable will not cover]

## 2. Spec and inputs

- Format and file: [for example, a Markdown file at `drafts/brief.md`]
- Length: [limit or range]
- Language and register: [for example, English, plain and direct]
- Inputs the worker must draw on:
  - [path or link, and what it is for]
- Must not be invented: [figures, quotations, citations and so on; anything not found in the inputs is flagged, not filled in]

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
  - Origin: [reference | user | suggested add | research]
- **C2. [Short name].** [Statement.]
  - Check: [how]
  - Origin: [origin]

### 4b. Benchmark comparison

The evaluator reads the draft next to the benchmark named in section 5. The draft must win or tie on every dimension. The benchmark may be about a different topic; each dimension is about craft, not subject matter.

- **D1. [Dimension].** [What "stronger" means on this dimension.]
- **D2. [Dimension].** [What "stronger" means.]

[If there is no benchmark, replace the list with: "No benchmark was available. The loop runs on the binary checks alone."]

## 5. Benchmark and references

- Benchmark for comparison: [path or link], [why the user rates it]
- What to emulate: [the specific qualities agreed with the user]
- What not to copy: [content, dated material, things the user would change today]
- Other references: [path or link, and what each is for]

## 6. Loop protocol

- Roles
  - Worker: the session that drafts and revises.
  - Evaluator: a fresh sub-agent started for each round. It receives the brief in section 7 and nothing else from the worker's conversation: no reasoning, no earlier evaluation reports.
  - Human: owns sections 3, 4 and 5.
- Each round
  - The worker writes or revises the draft at [draft path].
  - The worker starts a fresh evaluator with the section 7 brief, word for word.
  - The worker saves the evaluator's report to [eval dir]/round-N.md.
  - The worker revises to fix every failed check and every comparison the benchmark won.
- Human gate after round 1
  - The worker stops, shows the round 1 report, and asks whether the evaluator judged the right things.
  - The human confirms or amends the criteria. Amendments go in section 9.
  - After that the loop runs without check-ins.
- Stop when
  - every binary check passes and the benchmark wins no comparison dimension, or
  - round 5 has been evaluated.
- At the stop, the worker reports
  - the final result line from the last evaluation
  - any checks still failing, and why they resisted
  - any change to the criteria it would propose. It proposes; it does not edit.
- If the tool cannot start sub-agents
  - After each draft the worker stops and hands the human the section 7 brief to run in a separate, fresh session. The human pastes the report back.

## 7. Evaluator brief

Give this to the evaluator word for word.

> You are an independent evaluator. You did not write this draft and you have no stake in it passing.
>
> Read sections 1 to 5 of the plan at [plan path]. Read the draft at [draft path]. Read the benchmark at [benchmark path]. You may open the inputs listed in section 2 to verify claims.
>
> **Binary checks (section 4a).** Evaluate every check, every round, including ones that probably passed before. For each, give:
> - the verdict: PASS or FAIL
> - the evidence: a direct quote from the draft, with its location, that proves the verdict. For a check about something being absent, quote an instance to prove FAIL, or state what you searched for to prove PASS.
> - for a FAIL, one line on what is wrong. Do not rewrite the passage.
>
> If you cannot find evidence that a check passes, the verdict is FAIL.
>
> **Benchmark comparison (section 4b).** For each dimension, read both documents and say which is stronger: DRAFT, BENCHMARK or TIE. Support the call with one quote from each. The benchmark may be about a different topic; judge the craft the dimension names.
>
> **Result.** End with one line in this form:
> `CHECKS: [passed]/[total] · COMPARISON: [wins] wins, [ties] ties, [losses] losses · RESULT: DONE` or `REVISE`
>
> The result is DONE only if every check passes and there are no losses.
>
> Do not edit the draft. Do not grade generously: a human audits your first report against their own reading.

## 8. Assumptions and open questions

- [Assumption made where the user was not asked, or a question still open]

## 9. Change log

- [date]: plan agreed.
