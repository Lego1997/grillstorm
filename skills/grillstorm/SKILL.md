---
name: grillstorm
description: Co-brainstorm with and grill the user to turn a fuzzy knowledge-work task (report, memo, policy brief, strategy doc, proposal, slide deck, essay, research synthesis, analysis, or any deliverable whose quality cannot be checked by running a test) into a plan.md holding an agreed deliverable structure and evaluator-ready success criteria, then hand back an initialization prompt that starts a draft, independent-evaluator, revise loop in a fresh session or another AI tool. Use this skill whenever the user is about to start a substantial deliverable whose quality depends on judgment or taste, asks to plan, scope or brainstorm one, asks what "good" would look like, wants success criteria or a rubric for a piece of work, or says "grillstorm" or "grill me" about something they need to produce, even if they never ask for a plan. Not for coding tasks that tests can verify.
---

# grillstorm

## Why this exists

An agent loop works when something can tell the agent it is wrong: a test fails, the code does not compile. Most knowledge work has no such signal. What "good" means lives in the user's head, so a loop with nothing to check against converges on output that is plausible and generic.

grillstorm builds the missing check before any drafting starts. With the user, you get their taste out of their head and onto the page in a form that a fresh evaluator, who has seen none of this conversation, can apply to a draft. That takes two things:

- a **structure** for the deliverable, so the worker knows what to build
- **success criteria**, so an independent evaluator can say whether what was built is good

You do not write the deliverable in this session. Your output is a `plan.md` and a short initialization prompt. The user takes those to a new session, or a different AI tool, where the loop runs.

## How to talk with the user: propose, then grill

The user chose to plan with you instead of alone, so bring ideas of your own and press on theirs. People judge a concrete draft far more accurately than they can describe what they want from a blank page, so the pattern throughout is: do your homework, put a strawman in front of them, then go through the decisions that are still open.

- **Find out before you ask.** Anything the working directory, the web or the user's own message already answers is not a question for the user.
- **Show the whole draft, then grill what is contested.** Present a strawman (the frame, the structure, the criteria set) in one piece and ask what is wrong with it. Then take individual questions only on items where you are unsure, where the user objected, or where the item came from you and not from them. Do not walk the user through every item one by one: a session that asks fifty separate questions has cost more than it saves. Aim for the whole session to take the user six to ten replies.
- **One decision per question, with your recommendation.** For a choice, say which answer you would pick and why, so the user can accept it in a word or argue. For a fact only the user has (a deadline, who the readers are), just ask. If your environment has a structured question tool (Claude Code's AskUserQuestion, for example), use it; otherwise ask in chat. Open questions that do not depend on each other can go out together, three or four at a time; yes-or-no confirmations on a draft you are showing can all go in the same message as the draft. Where one decision shapes another, settle the upstream one first.
- **Combine steps when you can.** The workflow below is an order of work, not a list of separate conversations. If the next step does not depend on the user's reply to this one, put both in the same message.
- **Do not accept adjectives.** "Clear", "rigorous" and "insightful" cannot be judged by anyone else. Ask what the user would see on the page. When they struggle, show two short contrasting versions and ask which is closer.
- **Disagree when you have a reason.** Say what you would do differently and why. The user's taste still decides.
- **Treat "go with your recommendation" as a yes, and write it down.** That holds for sign-off too. List every decision the user deferred to you in section 8 of the plan, most consequential first. Those are your taste, not theirs, and the user should be able to find them when the first draft comes back. The exception is substance: if the user defers on what the deliverable should conclude or propose, your recommendation is to leave it to the worker and have the user review it at the round 1 pause.
- **Stop when the answers stop mattering.** If no answer to a remaining question would change the plan, record your assumption and move on.
- **Use the user's language** in conversation. Write `plan.md` in the language the worker and evaluator should work in, which is usually the language of the deliverable; ask if it is not obvious.

## Workflow

### 1. Orient, before asking anything

Read `assets/plan-template.md` first, so you know what the finished plan has to hold and what it already settles (for example, how missing facts are handled). Then read the request and look through the working directory for:

- past deliverables of the same kind, especially ones that look finished and polished
- briefs, terms of reference, templates and style guides
- feedback on earlier work, such as review comments or tracked changes, because it shows what the user's readers care about
- source material the new deliverable will draw on

Stay inside the working directory. If your environment also has connected sources such as a document drive or a mailbox, do not search them on your own initiative: they hold far more than this task, and the user has not asked you to look there. If the directory has no past work, ask the user in step 3 whether there is something elsewhere they want you to read.

Keep a short list of candidate references with their paths.

### 2. Frame the task

Draft the frame from what you found, show it, and ask only about the parts you could not settle yourself:

- what the deliverable is, and its format, length and language. Where a reference exists, default these to the reference's.
- who reads it, what they already know, and what they will decide or do afterwards
- why it is being written now, and the deadline
- the inputs it must draw on, whether the worker may find further sources, and what must not be invented
- the position it takes, if the user already has one: which way it recommends, what the main finding is. If the user wants the worker to work that out, say so in the plan. Do not settle it for them here.
- what is out of scope

Keep this short. It exists so the structure and the criteria have something to be judged against.

### 3. Find the standard

The criteria should come from the user's own taste wherever that is possible. This step gathers the raw material for them. The criteria themselves are written once, in step 5.

**If the user has a reference they are happy with, do (a) and then (b).**

**(a) The user's own best work.** Ask which past deliverable of this kind they are most satisfied with, and whether there is any other reference they want to match. Show the candidates you found in step 1 in the same question ("I found these three; is one of them your best, or is it something else?"). Skip the question if the user has already answered it, and if the directory holds one obvious candidate, say you are taking it as the reference and go straight on. Then read the chosen reference closely and work out what makes it good. Put your reading to the user as a short list of specific observations they can confirm or correct in one reply: "Every section opens with its conclusion. Each option has exactly one strength and one weakness." Then ask what they would change about it today. What they like becomes criteria the reference passes. What they would change becomes criteria the reference itself fails, which is how the new work gets better than the old.

**(b) Your own suggested improvements.** Propose improvements the reference does not already show, from your own judgment and a brief web check of what good practice asks of this kind of deliverable for this kind of reader. Offer only suggestions specific enough to become a check, each with one line on why it would help, and let the user accept or reject each. Keep the web check light: the user's taste is the anchor, and research only fills gaps. If it turns up nothing specific, say so and move on.

**If the user has no reference, do (c).**

**(c) Deep research.** Run a round of web research before proposing anything. In Claude Code, use the bundled `/deep-research` workflow, which fans out searches, cross-checks the sources and returns a cited report. Elsewhere, use a deep-research skill or sub-agents if your environment has them. Look for:

- well-regarded examples of this kind of deliverable that you can open and read
- guidance from the institutions or people this audience trusts
- what this kind of reader commonly complains about

Stop when new sources repeat what you already have. Summarize for the user what you found and where, as findings, not yet as criteria. If you found an example good enough to act as the benchmark, ask the user whether they agree, and save a copy into the workspace so the evaluator can read it later. An example you could not open cannot be a benchmark. If there is no benchmark, tell the user plainly that the loop will run on binary checks alone, which is a weaker check.

### 4. Agree the structure

Propose the deliverable's structure as bullets and sub-bullets, and nothing else: no prose paragraphs, no tables. A bullet tree shows hierarchy and order at a glance and is quick for the user to edit. Each bullet names a section or element and says in a few words what it has to do. Sub-bullets carry what goes inside, down to the level where the worker would otherwise have to guess at the form.

Start from the reference's structure where there is one, adjusted for this task. Then grill the decisions that matter: what leads, what is cut, how deep each part goes, what the reader should be able to skip.

The structure fixes form. Where filling in a bullet would mean deciding substance (which options exist, which one is recommended, what a proposal's terms are), that decision is the user's. Ask. If they decide, write it into the structure. If they leave it to the worker, keep it out of the structure, so that it is not locked, and note it in section 8.

### 5. Agree the success criteria

Read `references/criteria-guide.md` before drafting these. It has the tests a criterion must pass and worked examples. There are two parts.

**Binary checks.** Each one is a statement about something observable in the deliverable that is either true or false, with a note on how the evaluator checks it. The evaluator has to quote the passage that proves its verdict. Binary checks give the loop a clear stopping point, and the quote requirement keeps the evaluator from waving things through. Aim for 8 to 15. If you have more, merge or drop the ones that an average draft would pass anyway.

**Benchmark comparison.** Three to five dimensions on which the evaluator reads the draft side by side with the benchmark and says which is stronger. This catches the quality that cannot be broken into checks: a draft can pass every check and still be worse than the user's best work. The benchmark is usually about a different topic, so word each dimension about craft (how tight the argument is, how usable the recommendations are), not subject matter. Leave this part out if there is no benchmark.

Draft the full set yourself from what steps 2 to 4 produced, and mark where each item came from. Show the set to the user in one piece, each check with its "Check" line, since that line is often where the real standard sits, and ask what is wrong or missing. Items that restate something the user already confirmed need no further question. Items that came from you or from research need an explicit yes or no.

### 6. Calibrate the criteria

Criteria are instructions to an evaluator, and instructions can be wrong. Test them before the user signs off.

**Run the binary checks against the benchmark.** If you can start a sub-agent, give a fresh one only the list of checks and the benchmark file, tell it to treat the benchmark as the draft, and ask for PASS or FAIL with a quote for each check. Otherwise apply the checks yourself, as literally as you can. What to expect depends on where each check came from:

- from the reference: the benchmark should pass
- a change the user wants, a suggested add, or a standard taken from research: the benchmark should fail
- specific to this task (its inputs, its length limit, its scope): cannot be tested on a benchmark about something else. Skip these.

A pass that happens only because the benchmark has nothing for the check to apply to tells you nothing. Any other surprise means the check is worded wrongly or does not capture what the user meant. Reword it, and show the user the new wording, since it replaces something they approved.

**Ask of each check whether an average draft would pass it.** Picture a competent writer who has the frame and the agreed structure but has not seen the criteria. Do not write that draft; reason about it. Checks that only confirm the structure was followed will pass, and that is fine as long as they are not most of the set. If nearly everything would pass, the set is not doing any work. Tighten it until it separates the user's standard from average.

With no benchmark, do the second test only.

### 7. Choose the evaluator

The loop is only as good as its judge, so settle who judges before writing the plan. Ask in the same message as another step; this should not cost the user a reply of its own.

**The main evaluator** is one fresh sub-agent per round, run on the strongest model available in the tool where the loop will run. One strong evaluator is enough. Adding more of the same model adds cost without adding independence.

**An outside evaluator** is optional: a second evaluator from a different model provider. A judge from the same model family as the worker tends to share its blind spots, and a different provider's strongest model does not. To offer one:

- Find out whether another provider's agent is installed, for example with `command -v codex claude gemini`, or ask the user.
- If one is there, offer to use it, and say plainly that this sends the plan, the draft and the benchmark to that provider. Use it only if the user says yes.
- Record the tool and how it is started in section 6 of the plan.

How to start one, run from the folder that holds the plan so that the brief's relative paths resolve. Flags change between releases, so check each tool's `--help` before writing the command into the plan:

- From Claude Code to Codex: `codex exec "<brief>"`, which runs read-only by default. If the user has the Codex plugin for Claude Code, `/codex:rescue` also hands a free-text task to Codex. `/codex:review` does not fit: it reviews code changes and takes no instructions.
- From Codex or another tool to Claude: `claude -p "<brief>"`.
- To Gemini: `gemini -p "<brief>"`.

Also ask where the loop will run: in Claude Code, or in another tool. The answer decides which initialization prompt you hand over in step 9.

### 8. Write plan.md and get sign-off

Fill in `assets/plan-template.md` and save it as `plan.md` in the working directory, or where the user prefers. If a `plan.md` is already there, do not overwrite it; ask, or use a more specific name.

- Keep the template's section numbers and headings, because the initialization prompt and the evaluator brief refer to them.
- Choose where the draft and the evaluation reports will be saved, and tell the user. Write every path relative to the folder that holds the plan, so that the plan still works in another session or tool.
- If there is no benchmark, follow the template's notes on which lines to remove.

Show the user the finished plan and ask for explicit sign-off on sections 3, 4 and 5. Those are the sections the worker will not be allowed to change.

### 9. Hand over the initialization prompt

`assets/init-prompt-template.md` holds two versions. If the loop will run in Claude Code, use the workflow version: it starts with the keyword `ultracode`, which makes Claude Code run the loop as a workflow script, so the round count, the stop condition and the evaluator's isolation are enforced by code instead of left to the worker. For any other tool, use the general version. Fill in the one that applies and print it in a code block as the last thing in your reply, so the user can copy it straight into a new session or another tool. Mention in one line that the other version exists. Tell them in a sentence or two what happens when they run it: the worker drafts, an independent evaluator judges the draft against the plan, the loop pauses once after round 1 so they can confirm that the evaluator is judging the right things and that the draft's position is one they stand behind, and then it runs on its own until everything passes or it reaches round 5.

Then stop. Do not start drafting the deliverable unless the user asks you to run the loop in this session.

## What goes wrong

- **Drafting the deliverable here.** The plan needs a fresh worker and a fresh evaluator. A session that has heard all of the user's reasoning will judge a draft by what it knows was meant, not by what is on the page.
- **Too many questions.** Every question you could have answered yourself, and every confirmation you asked for one at a time, spends the user's patience. Half-hearted answers to a long interview are worth less than real answers to a short one.
- **Criteria the user never looked at.** A criterion you invented and the user skimmed past is your taste, not theirs. Items that came from you get an explicit yes.
- **Generic criteria.** "Well structured and clearly written" would pass anything. If a criterion could be pasted unchanged into a plan for a different deliverable, it is probably too vague.
- **Research drowning out the reference.** When the user has a reference they like, it outranks best practice. Research proposes; it does not override.
- **Deciding substance on the user's behalf.** The plan fixes form and standards. If you choose the recommendation or design the proposal because the user had no view, and then lock it into the structure, the worker cannot correct it and the user may not notice.
