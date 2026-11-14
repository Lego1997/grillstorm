# Writing success criteria an evaluator can apply

The evaluator is a fresh agent. It has the plan, the draft, the benchmark and the listed sources. It has not heard the user explain anything. A criterion works only if that reader can apply it and reach the verdict the user would reach.

## Tests for a binary check

A check is ready when it passes all five.

- **Observable.** It is about something on the page, not about the writer's intent or the reader's feelings. "The reader feels confident" fails this test. "Each recommendation names who acts and by when" passes.
- **One verdict.** It asks for a single pass or fail. A check may have several parts when they belong to one standard and the "Check" line lists them ("names the actor, the action and a time frame"). Split a check only when the parts are separate standards that the user would care about separately.
- **Quotable.** The evaluator can point at a passage that proves pass or fail. For checks about something being absent ("no unexplained acronyms"), the evaluator proves a fail by quoting an instance and a pass by stating what it searched for.
- **Discriminating.** A competent but generic first draft would plausibly fail it. A check that everything passes costs evaluator attention and tells the loop nothing.
- **Self-contained.** It can be applied with only what the evaluator can reach. If it depends on something the user said in conversation, write that into the check. If it depends on opening web links, remember that the evaluator may have no web access, in which case the check fails every round; where you can, have it rely on files in the workspace instead.

## Turning vague wishes into checks

Ask the user what they would see on the page, then write that down.

- "The summary should be strong."
  - Check: The summary states the main recommendation in its first two sentences.
  - Check: A reader who stops after the summary knows what is being asked of them and why. The evaluator states the ask in one sentence using the summary alone.
- "It should be evidence-based."
  - Check: Every quantitative claim carries a source the reader can open.
  - Check: Each of the main findings is supported by at least one piece of evidence from the listed inputs, not only by general reasoning.
- "Don't make it sound like AI wrote it."
  - Check: No paragraph opens with a restatement of the paragraph before it.
  - Check: No sentence could be deleted without losing information. The evaluator quotes any that could.
- "It should be balanced."
  - Check: The strongest objection to the main recommendation is stated in terms its proponents would accept, and is answered.
- "Two pages at most."
  - Check: The draft is at most 850 words. Page counts cannot be checked in a text file, so convert them to a word count and tell the user the number you chose.

## What a check looks like in plan.md

- **C4. Recommendations are actionable.** Every recommendation names the actor, the action and a time frame.
  - Check: List each recommendation and mark which of the three parts are present. Fail if any part is missing from any recommendation.
  - Origin: reference

The "Check" line tells the evaluator how to do the check, so two evaluators would do it the same way.

The "Origin" line lets the user see later where each standard came from, and tells you what to expect in calibration. It is one of:

- **reference**: something the benchmark already does and the user confirmed they want
- **user**: something the user asked for that is not about the benchmark, such as a length limit or a scope rule
- **user change**: something the user would do differently from the benchmark today
- **suggested add**: proposed by the planning session and accepted by the user
- **research**: taken from a source found in research and accepted by the user

## Coverage

Before showing the set to the user, look across these areas and ask whether one that matters for this deliverable has no check. Not every area needs one.

- **Substance.** Does it answer the question that was asked? Is what must be included there?
- **Reasoning.** Do the conclusions follow? Are alternatives and objections dealt with?
- **Evidence.** Are claims sourced? Is anything invented? Are the listed inputs used?
- **Audience fit.** Can this reader use it, with their knowledge and their time?
- **Structure.** Does it follow section 3 of the plan? Is the order doing work?
- **Voice.** Does it sound like the user's own work?
- **Format.** Length, layout, citation style, file type.

## Benchmark comparison dimensions

Checks cannot capture everything. A draft can pass all of them and still read worse than the user's best work. The comparison covers that gap.

- Pick three to five dimensions. Name the things the user said they like most about the benchmark.
- Word them about craft, since the benchmark usually has a different topic: "how quickly a reader gets to the main point", "how much each paragraph adds", "how concrete the recommendations are".
- Say what "stronger" means in one line each, so the evaluator is not left to guess.
- The rule for the loop is that the draft must win or tie on every dimension. The evaluator quotes one passage from each document to support its call.

Example:

- **D2. Density.** Which document gives the reader more usable content per page? Stronger means fewer sentences that restate, hedge or set up.

## When there is no benchmark

Leave the comparison out and say so in the plan. Compensate by making the binary checks stricter and by leaning on the average-draft test: if an average draft would pass most of the checks, they need tightening.

## Calibration results and what to do with them

- **The benchmark fails a check of origin "reference".** The wording is stricter than what the benchmark actually does, or the evaluator read it differently from how the user meant it. Reword the check and show the user the new wording.
- **The benchmark passes a suggested add or a user change.** If it passes because it really does the thing, the reference already meets this standard: change the origin to "reference". If it passes only because there was nothing for the check to apply to (a check about explaining technical terms, run on a benchmark that has none), the result tells you nothing; leave the check as it is.
- **A check is specific to this task.** Checks about this task's inputs, length or scope cannot be tested on a benchmark about something else. Skip them and note in section 8 that round 1 is their first real test.
- **You ran the checks twice and the two runs disagree.** The check leaves too much to judgment. Add detail to the "Check" line or split the check.
- **An average draft would pass nearly everything.** The checks are too easy. Ask the user what separates their best work from an acceptable piece, and write that down.
