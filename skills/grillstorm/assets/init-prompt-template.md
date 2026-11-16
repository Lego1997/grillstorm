# Initialization prompt templates

There are two versions. Use the workflow version when the loop will run in Claude Code, and the general version for any other tool. Fill in the bracketed parts and print the result in a code block as the last thing in your reply.

Keep the prompt short: everything of substance is in the plan, and the prompt only has to point the new session at it and name the rules that must not be bent.

Adjust either version to the plan:

- If there is no benchmark, drop the phrase about comparison dimensions.
- If the plan names an outside evaluator, keep the lines about it. If it does not, delete them.

## General version

For Codex, Cursor and any other tool. The worker runs the loop itself and starts a fresh sub-agent as the evaluator.

```
Read [plan path] in full before you do anything else. It is the agreed plan for [deliverable, in a few words]. I settled its structure, success criteria and loop protocol in an earlier planning session, so treat them as fixed.

Produce the deliverable at [draft path] by running the loop in section 6 of the plan:

1. Draft to the structure in section 3, using the inputs in section 2.
2. After each draft, start a fresh, independent evaluator sub-agent on the strongest model you have. Give it the brief in section 7 word for word, and nothing from this conversation. Save its report to [eval dir]/round-N.md. If you cannot start sub-agents, stop and give me the brief so I can run it in a separate session.
3. Also give the same brief to the outside evaluator named in section 6, and add its report to the same file. A check passes only if both evaluators pass it; list any they disagree on as contested.
4. After round 1, stop and show me the draft and the evaluator's report, so I can confirm the evaluator is judging the right things and that I stand behind the position the draft takes.
5. Once I confirm, keep revising and re-evaluating without checking in, until every binary check passes and the draft wins or ties every comparison dimension, or until round 5 has been evaluated.
6. Then tell me the final result, any checks still failing and why, every gap you flagged that I still have to fill, and any changes to the criteria you would propose.

Do not edit sections 3, 4 or 5 of the plan. If you think a criterion is wrong, say so in your report and carry on. Only I change the criteria.
```

## Workflow version, for Claude Code

The prompt opens with the keyword `ultracode`, which asks Claude Code to run the task as a dynamic workflow: a script that starts the agents, holds the loop and decides when to stop. That takes the round count, the stop condition and the evaluator's isolation out of the worker's hands.

Two things about workflows shape this prompt. A workflow run cannot stop for the user's input, so the pause after round 1 is the gap between two runs. And the keyword counts only when the user sends the prompt themselves at the Claude Code prompt, so tell the user to paste it there and not to pass it through another agent.

```
ultracode: read [plan path] in full before you do anything else. It is the agreed plan for [deliverable, in a few words]. I settled its structure, success criteria and loop protocol in an earlier planning session, so treat them as fixed.

Produce the deliverable at [draft path] by running the loop in section 6 of the plan as workflows. A workflow cannot stop for my input, so use two runs.

Run 1 covers round 1 only:
- One agent drafts to the structure in section 3, using the inputs in section 2, and saves the draft.
- Then one fresh evaluator agent, on the strongest model available, receives the brief in section 7 word for word and nothing else. It returns structured output: for each check its id, verdict, evidence and note; for each comparison dimension its call; and the result line. It saves its full report to [eval dir]/round-1.md.
- A second agent gives the same brief to the outside evaluator named in section 6 and adds that report to the same file. A check passes only if both evaluators pass it; list any they disagree on as contested.
- End the run and show me the draft and the report. Wait for me to confirm that the evaluator is judging the right things and that I stand behind the position the draft takes.

Run 2 starts after I confirm and covers rounds 2 to 5:
- In each round, one agent revises the draft to fix everything the latest report marks as failed, contested or lost. Give it the plan, the current draft and the latest report, and nothing else.
- Then a fresh evaluator judges the new draft exactly as in round 1, and the report is saved to [eval dir]/round-N.md.
- The script reads the evaluator's structured result and decides whether to stop. It stops when every binary check passes and the draft wins or ties every comparison dimension, or when round 5 has been evaluated. The revising agent does not make that call.

When run 2 ends, tell me the final result, any checks still failing and why, every gap flagged in the draft that I still have to fill, and any changes to the criteria you would propose.

No agent may edit sections 3, 4 or 5 of the plan. If an agent thinks a criterion is wrong, it says so in its report and carries on. Only I change the criteria.
```
