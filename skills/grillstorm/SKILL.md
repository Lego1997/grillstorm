---
name: grillstorm
description: Co-brainstorm with and grill the user to turn a fuzzy knowledge-work task (report, memo, policy brief, strategy doc, proposal, slide deck, essay, research synthesis, analysis, or any deliverable whose quality cannot be checked by running a test) into a plan.md holding an agreed deliverable structure and evaluator-ready success criteria, then hand back an initialization prompt that starts a draft, independent-evaluator, revise loop in a fresh session or another AI tool. Use this skill whenever the user is about to start a substantial deliverable whose quality depends on judgment or taste, asks to plan, scope or brainstorm one, asks what "good" would look like, wants success criteria or a rubric for a piece of work, or says "grillstorm" or "grill me" about something they need to produce, even if they never ask for a plan. Not for coding tasks that tests can verify.
---

# GrillStorm

## Why this exists

An agent loop works when something can tell the agent it is wrong: a test fails, the code does not compile. Most knowledge work has no such signal. What "good" means lives in the user's head, so a loop with nothing to check against converges on output that is plausible and generic.

GrillStorm builds the missing check before any drafting starts. With the user, you get their taste out of their head and onto the page in a form that a fresh evaluator, who has seen none of this conversation, can apply to a draft. That takes two things:

- a **structure** for the deliverable, so the worker knows what to build
- **success criteria**, so an independent evaluator can say whether what was built is good

You do not write the deliverable in this session. Your output is a `plan.md` and a short initialization prompt. The user takes those to a new session, or a different AI tool, where the loop runs.

## How to talk with the user: propose, then grill

The user chose to plan with you instead of alone, so bring ideas of your own and press on theirs. People judge a concrete draft far more accurately than they can describe what they want from a blank page, so the pattern throughout is: do your homework, put a strawman in front of them, then go through the open decisions.

- **Find out before you ask.** Anything the workspace or the web can answer is not a question for the user. Their time goes to the decisions only they can make.
- **One decision per question, with your recommendation.** Say which answer you would pick and why, so the user can accept it in one word or argue with it. If your environment has a structured question tool (Claude Code's AskUserQuestion, for example), use it; otherwise ask in chat. Questions that do not depend on each other can go out together, three or four at most. Where one decision shapes another, settle the upstream one first.
- **Do not accept adjectives.** "Clear", "rigorous" and "insightful" cannot be judged by anyone else. Ask what the user would see on the page. When they struggle, show two short contrasting versions and ask which is closer.
- **Disagree when you have a reason.** Say what you would do differently and why. The user's taste still decides.
- **Stop when the answers stop mattering.** If no answer to a remaining question would change the plan, record your assumption in the plan and move on.
- **Use the user's language** in conversation. Write `plan.md` in the language the worker and evaluator should work in, which is usually the language of the deliverable; ask if it is not obvious.

## Workflow

### 1. Orient, before asking anything

Read the request, then look around the workspace: the working directory, and any document sources the user has connected for this work. You are looking for:

- past deliverables of the same kind, especially ones that look finished and polished
- briefs, terms of reference, templates and style guides
- feedback on earlier work (review comments, tracked changes, emails), because it shows what the user's readers care about
- source material the new deliverable will draw on

Keep a short list of candidate references with their paths. You will show it to the user in step 3.

### 2. Frame the task

Draft the frame from what you found, show it, and grill only the parts you could not settle yourself:

- what the deliverable is, and its format, length and language
- who reads it, and what they will decide or do afterwards
- why it is being written now, and the deadline
- the inputs it must draw on, and anything it must not invent
- what is out of scope

Keep this short. It exists so the structure and the criteria have something to be judged against.

### 3. Find the benchmark

The criteria should come from the user's own taste wherever that is possible. Work down this order of preference and stop at the first level that gives you enough.

**(a) The user's own best past work.** Ask the user which past deliverable of this kind they are most satisfied with, and whether there is any other reference they want to match. Ask this alongside showing the candidates you found in step 1 ("I found these three; is one of them your best, or is it something else?"). Then read the chosen reference closely and work out what makes it good. Put your reading to the user as specific observations they can confirm or correct: "Every section opens with its conclusion. Is that deliberate?" Also ask what they would change about it today. What they like becomes criteria; what they would change becomes criteria the reference itself would fail, which is how the new work gets better than the old.

**(b) Your own suggested improvements.** With the reference understood, propose improvements it does not already show. Draw on your own judgment and on a brief web check of what good practice for this kind of deliverable and audience asks for. Offer each one separately, with one line on why it would help, and let the user accept or reject it. Accepted ones become criteria marked as suggested adds. Keep the web check light here: the user's taste is the anchor, and research only fills gaps.

**(c) No reference at all.** If the user has nothing they are happy with and nothing they want to match, run a round of deep web research before proposing anything. Look for well-regarded examples of this kind of deliverable, guidance from the institutions or people this audience trusts, and what this kind of reader tends to complain about. Use a deep-research skill or sub-agents if your environment has them. Then propose a criteria set with the source for each item, and grill the user on whether each is right for them. Ask whether one of the examples you found can serve as the benchmark for comparison. If none can, say plainly that the loop will run on binary checks alone, which is a weaker check.

### 4. Agree the structure

Propose the deliverable's structure as bullets and sub-bullets, and nothing else: no prose paragraphs, no tables. A bullet tree shows hierarchy and order at a glance and is quick for the user to edit. Each bullet names a section or element and says in a few words what it has to do. Sub-bullets carry what goes inside, down to the level where the worker would otherwise have to guess.

Start from the reference's structure where there is one, adjusted for this task. Then grill the decisions that matter: what leads, what is cut, how deep each part goes, what the reader should be able to skip.

### 5. Agree the success criteria

Read `references/criteria-guide.md` before drafting these. It has the tests a criterion must pass and worked examples. There are two parts.

**Binary checks.** Each one is a statement about something observable in the deliverable that is either true or false, with a note on how the evaluator checks it. The evaluator has to quote the passage that proves its verdict. Binary checks give the loop a clear stopping point, and the quote requirement keeps the evaluator from waving things through. Aim for 8 to 15; with more, the important ones get lost.

**Benchmark comparison.** Three to five dimensions on which the evaluator reads the draft side by side with the benchmark and says which is stronger. This catches the quality that cannot be broken into checks: a draft can pass every check and still be worse than the user's best work. The benchmark is usually about a different topic, so word each dimension about craft (how tight the argument is, how usable the recommendations are), not subject matter.

Draft both parts yourself from steps 3 and 4, mark where each item came from (reference, user, suggested add, research), then go through them with the user one at a time.

### 6. Calibrate the criteria

Criteria are instructions to an evaluator, and instructions can be wrong. Test them before the user signs off:

- **Run the binary checks against the benchmark itself.** Use a fresh sub-agent with the evaluator brief if you can, otherwise do it yourself. The benchmark should pass every check that was derived from it and fail only the suggested adds and the things the user said they would change. Any other result means a criterion is worded wrongly or does not capture what the user meant. Show the user the surprises and fix the wording together.
- **Ask of each check: would a competent but generic first draft pass it?** If nearly all of them would pass, the criteria are not doing any work. Tighten them until they separate the user's standard from average.

With no benchmark, do the second test only.

### 7. Write plan.md and get sign-off

Fill in `assets/plan-template.md` and save it as `plan.md` in the workspace, or where the user prefers. If a `plan.md` is already there, do not overwrite it; ask, or use a more specific name. Keep the template's section numbers and headings, because the initialization prompt and the evaluator brief refer to them. Fill in the loop protocol and the evaluator brief with the real file paths.

Show the user the finished plan and ask for explicit sign-off on sections 3 and 4. Those are the two sections the worker will not be allowed to change.

### 8. Hand over the initialization prompt

Fill in `assets/init-prompt-template.md` and print it in a code block as the last thing in your reply, so the user can copy it straight into a new session or another tool. Tell them in a sentence or two what happens when they run it: the worker drafts, an independent evaluator judges the draft against the plan, the loop pauses once after round 1 so they can confirm the evaluator is judging the right things, and then it runs on its own until everything passes or it reaches round 5.

Then stop. Do not start drafting the deliverable unless the user asks you to run the loop in this session.

## What goes wrong

- **Drafting the deliverable here.** The plan needs a fresh worker and a fresh evaluator. A session that has heard all of the user's reasoning will judge a draft by what it knows was meant, not by what is on the page.
- **Criteria the user never looked at.** A criterion you invented and the user skimmed past is your taste, not theirs. Every criterion gets a yes from the user.
- **Generic criteria.** "Well structured and clearly written" would pass anything. If a criterion could be pasted into a plan for a different deliverable unchanged, it is probably too vague.
- **Research drowning out the reference.** When the user has a reference they like, it outranks best practice. Research proposes; it does not override.
- **Asking a long list of questions before showing anything.** Show a strawman early. Corrections come faster than answers.
