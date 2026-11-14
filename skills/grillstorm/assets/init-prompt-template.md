# Initialization prompt template

Fill in the bracketed parts and print the result in a code block as the last thing in your reply. Keep it short: everything of substance is in the plan, and the prompt only has to point the new session at it and name the rules that must not be bent. If there is no benchmark, drop the phrase about comparison dimensions from step 4.

```
Read [plan path] in full before you do anything else. It is the agreed plan for [deliverable, in a few words]. I settled its structure, success criteria and loop protocol in an earlier planning session, so treat them as fixed.

Produce the deliverable at [draft path] by running the loop in section 6 of the plan:

1. Draft to the structure in section 3, using the inputs in section 2.
2. After each draft, start a fresh, independent evaluator sub-agent. Give it the brief in section 7 word for word, and nothing from this conversation. Save its report to [eval dir]/round-N.md. If you cannot start sub-agents, stop and give me the brief so I can run it in a separate session.
3. After round 1, stop and show me the evaluator's report, so I can confirm it is judging the right things.
4. Once I confirm, keep revising and re-evaluating without checking in, until every binary check passes and the draft wins or ties every comparison dimension, or until round 5 has been evaluated.
5. Then tell me the final result, any checks still failing and why, and any changes to the criteria you would propose.

Do not edit sections 3, 4 or 5 of the plan. If you think a criterion is wrong, say so in your report and carry on. Only I change the criteria.
```
