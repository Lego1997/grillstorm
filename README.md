# GrillStorm

GrillStorm is an agent skill for AI coding tools (Claude Code, Codex, Cursor and others that read the open Agent Skills format). It runs a planning conversation with you before any drafting starts, and hands you a `plan.md` and a short initialization prompt. You paste that prompt into a fresh session or another tool, where a draft, independent-evaluator, revise loop does the work.

Version 0.1.0. [MIT License](LICENSE).

## The problem

Agent loops work well when the outcome can be verified: the agent writes code, a test fails, the agent fixes it. Reports, memos, policy briefs, strategy documents and slide decks have no test. What "good" means is in your head, so a loop with nothing to check against settles on output that is plausible and generic.

GrillStorm builds the missing check first. In one planning conversation, you and the model agree on:

1. **A structure** for the deliverable, written strictly as bullets and sub-bullets.
2. **Success criteria** that an independent evaluator sub-agent can apply to a draft, without having seen the planning conversation.

The criteria have two parts: binary checks (each backed by a quoted passage from the draft) and, when you have past work to compare against, a side-by-side comparison on a few dimensions of craft. Together they give the loop something concrete to test against.

## What a session looks like

1. **The model does its homework.** It reads your working directory for past deliverables, briefs, style guides, feedback on earlier work and source material. It stays inside the directory and does not search connected sources such as a document drive or mailbox unless you point it there.

2. **It proposes, then grills.** It puts a strawman in front of you: a frame for the task, a draft structure, a draft set of criteria. It asks what is wrong with it. Individual questions come only where you disagree, where something is unknown, or where a decision came from the model rather than from you. Criteria draw first on your own best past work, then on improvements the model suggests (from its judgment and a light web check) that you accept or reject one by one. Deep web research fills in only when you have no reference at all.

3. **You agree the criteria.** The model calibrates them by running the binary checks against your reference. If your best work fails a check that was derived from it, the check is worded wrongly and gets fixed. If nearly every check would pass an average draft, the set is too easy and gets tightened.

4. **You get `plan.md` and an initialization prompt.** The plan holds the goal, spec, structure, success criteria, benchmark, loop protocol, an evaluator brief and a record of every decision you left to the model. The skill does not decide what the deliverable should conclude or recommend; that is left to you or to the worker. The prompt is a short block of text you paste into a new session or another tool.

The whole planning conversation aims for six to ten replies from you.

## How the criteria work

### Binary checks

Each check is a statement about something observable in the draft that is either true or false. The evaluator must quote the passage that proves its verdict. It cannot wave a check through without evidence.

**Example.** For a policy brief, a check might read:

> **C4. Recommendations are actionable.** Every recommendation names the actor, the action and a time frame.
> - Check: List each recommendation and mark which of the three parts are present. Fail if any part is missing from any recommendation.

Compare this with "Recommendations are clear and useful", which any draft could claim to pass. The check tells the evaluator exactly what to look for, so two evaluators would reach the same verdict.

### Benchmark comparison

If you have a past deliverable you are satisfied with, the evaluator reads the new draft next to it and says which is stronger on three to five dimensions of craft. The benchmark is usually about a different topic, so dimensions are about how the work is done, not what it is about.

**Example.**

> **D2. Density.** Which document gives the reader more usable content per page? Stronger means fewer sentences that restate, hedge or set up.

A draft can pass every binary check and still read worse than your best work overall. The comparison catches that gap. When no reference is available, the loop runs on binary checks alone.

## The loop the initialization prompt starts

When you paste the prompt into a fresh session:

1. The worker drafts the deliverable to the agreed structure.
2. It starts a fresh, independent evaluator sub-agent with the evaluator brief from the plan. The evaluator sees the plan's goal, spec, structure, criteria and benchmark, plus the draft, but nothing from the worker's conversation.
3. **After round 1, the worker pauses.** You confirm that the evaluator is judging the right things and that the position the draft takes is one you stand behind. You may amend the criteria or settle the position; changes are recorded in the plan.
4. After you confirm, the loop runs without check-ins until every binary check passes and the draft wins or ties every comparison dimension, or until round 5 has been evaluated.
5. At the stop, the worker reports the final result, any checks still failing, every gap flagged for you to fill, and any changes to the criteria it would propose.

Only you can change the structure, the criteria and the benchmark. The worker may propose changes but cannot make them.

If the tool cannot start sub-agents, the worker pauses after each draft and gives you the evaluator brief to run in a separate session.

## Install

The skill is one folder, `skills/grillstorm/`, in the open Agent Skills format (a `SKILL.md` plus bundled files).

### Claude Code, as a plugin

```bash
claude plugin marketplace add Lego1997/grillstorm
```

```bash
claude plugin install grillstorm@grillstorm
```

Invoke with `/grillstorm:grillstorm`.

### Claude Code, as a personal skill

```bash
git clone https://github.com/Lego1997/grillstorm
```

```bash
mkdir -p ~/.claude/skills && cp -r grillstorm/skills/grillstorm ~/.claude/skills/
```

Invoke with `/grillstorm`.

### Cursor

Copy `skills/grillstorm/` to `.cursor/skills/grillstorm/` in your project. Cursor also reads `~/.claude/skills/`, so the personal Claude Code install above covers both.

### Codex

Copy `skills/grillstorm/` to `~/.agents/skills/grillstorm/` (older versions read `~/.codex/skills/`). Invoke with `$grillstorm`. Codex skill paths have moved between releases; check OpenAI's docs if this does not work.

### Other tools

Any tool that reads Agent Skills can use the folder as is. In a tool without skill support, paste the contents of `SKILL.md` as your first message and attach the files in `assets/` and `references/`.

## Usage

Start it when you are about to begin a substantial deliverable:

> /grillstorm I need to write a policy brief on compute governance for our board next week.

The skill does not write the deliverable. It stops after handing you the plan and the initialization prompt.

## Design choices

**Why binary checks with quoted evidence?** A check like "the writing is clear" lets the evaluator wave it through on impression. Requiring a quote for every verdict forces the evaluator to point at specific text. If it cannot find a passage that proves a check passes, the verdict is FAIL.

**Why compare against your own best work?** Binary checks test individual properties, but a draft can pass them all and still read worse than your best work overall. Side-by-side comparison on a few dimensions of craft catches quality that the checks miss: coherence, density, how quickly a reader gets to the point.

**Why calibrate against the reference before signing off?** Criteria are instructions to an evaluator, and instructions can be wrong. Running the checks against the benchmark before the loop starts catches wording that is stricter or looser than what you actually meant. A check derived from the reference should pass; one that represents a deliberate improvement should fail.

**Why not write the deliverable in the same session?** The evaluator has to judge a draft by what is on the page, not by what it heard you explain. A session that has heard all the planning reasoning will be generous with a draft it helped shape. The plan needs a fresh worker and a fresh evaluator.

## Status

The skill has been dry-run three times with simulated users: twice with a user who had a past brief as reference, once with a user who had no reference. Those runs produced complete plans and initialization prompts and led to two rounds of revisions to the skill's wording. It has not yet been used by a real person on a real deliverable. The evaluation loop that the initialization prompt starts has not been run end to end, and the latest wording changes have not been re-run. Treat it as an early draft.

## Repo layout

```
.claude-plugin/          plugin and marketplace manifests for Claude Code
skills/grillstorm/
  SKILL.md               the skill workflow
  assets/
    plan-template.md     the plan the skill fills in
    init-prompt-template.md
  references/
    criteria-guide.md    how to write criteria an evaluator can apply
```

## Credits

Inspired by Matt Pocock's [grill-me skill](https://github.com/mattpocock/skills), which interviews you about a plan one question at a time, and by co-brainstorming with AI as a way of working.

## 中文简介

GrillStorm 是用于 Claude Code、Codex、Cursor 等 AI 工具的 agent skill。它要解决的问题是：代码可以靠测试验证，适合让模型循环迭代；但报告、备忘录、政策简报这类知识工作没有测试可跑，循环无从判断好坏，产出容易流于空洞。

GrillStorm 在动笔之前先和你进行一轮结构化讨论，产出一份 `plan.md`，包含：

- 交付物的结构（严格使用层级要点）
- 成功标准：可由独立评估 sub-agent 逐条判定的二元检查项（每条必须引用原文为证据），以及与你最满意的过往作品在几个维度上的并排比较

标准优先取自你自己满意的过往作品，其次是模型提出、由你逐条取舍的改进建议；两者都没有时模型才做深度研究。签字前，模型用过往作品试跑检查项来校准：源自作品的检查项，作品应当通过，否则措辞有误；如果普通初稿也能通过大部分检查项，说明标准太松。

讨论结束后你会得到一段初始化提示词，贴到新 session 或其他工具中即可启动"起草 → 独立评估 → 修改"循环。第一轮后暂停一次请你确认评估方向和立场，此后自动运行至全部通过或第 5 轮。只有你可以修改结构、标准和参照作品。你委托模型做的决定记录在计划中，方便事后查阅；交付物的实质主张（结论、建议）留给你或执行者决定，不在规划阶段锁定。

注意：该 skill 只读取当前工作目录中的文件，不会主动搜索文档云盘或邮箱，除非你明确指向。

当前状态：版本 0.1.0，已用模拟用户干跑三次（两次有参考作品，一次没有），并据此修订了两轮措辞。尚未经真实用户在真实任务上使用，评估循环未完整跑通，最新措辞改动未重新测试。请视为早期草稿。

[MIT License](LICENSE).
