# GrillStorm

A skill for AI coding tools (Claude Code, Codex, Cursor and others) that plans knowledge work with you before any drafting starts. It ends with a `plan.md` and a short prompt you paste into a fresh session, where a draft, evaluate, revise loop does the work.

## The problem

Agent loops work well when the outcome can be verified: the agent writes code, a test fails, the agent fixes it. Reports, memos, policy briefs, strategy documents and slide decks have no test. What "good" means is in your head, so a loop has nothing to check against and settles on output that is plausible and generic.

GrillStorm builds the missing check first. In one planning conversation, you and the model agree on:

1. **The structure of the deliverable**, written strictly as bullets and sub-bullets.
2. **Success criteria** that an independent evaluator sub-agent can apply to a draft:
   - binary checks, each of which the evaluator must support with a quote from the draft
   - a side-by-side comparison against your own best past work

## How the conversation goes

The model proposes, then grills. It reads your working directory first, puts a strawman in front of you, and then takes the contested decisions one at a time, each with its own recommended answer. It does not search connected sources such as a document drive or mailbox unless you point it there.

The criteria come from your taste wherever possible, in this order:

1. **Your best past work.** The model asks which past deliverable you are most satisfied with, looks through your working directory for candidates, and works out with you what makes the chosen one good.
2. **Suggested improvements.** The model proposes improvements beyond the reference, from its own judgment and a light web check. You accept or reject each.
3. **Deep research.** Only if you have no reference at all, the model researches what good looks like for this kind of deliverable and reader, proposes criteria with sources, and goes through them with you.

Before you sign off, the model calibrates the criteria by running them against the reference itself. If your best work fails a check that was derived from it, the check is worded wrongly and gets fixed.

## What you get

- `plan.md`: goal, spec and inputs, structure, success criteria, benchmark, the loop protocol, and a brief for the evaluator.
- An initialization prompt, printed in chat. Paste it into a new session or another tool. It tells the worker to:
  - draft to the agreed structure
  - have a fresh, independent evaluator judge each draft against the plan
  - pause once after round 1, so you can confirm the evaluator is judging the right things and that you stand behind the position the draft takes
  - then run on its own until every check passes and the draft wins or ties the comparison, or until round 5

Only you can change the structure and the criteria. The worker may propose changes but cannot make them.

## Install

The skill is one folder, `skills/grillstorm/`, in the open Agent Skills format (a `SKILL.md` plus bundled files). Skill paths have moved between tool releases, so check your tool's documentation if a path below does not work.

**Claude Code, as a plugin**

```bash
claude plugin marketplace add Lego1997/grillstorm
```

```bash
claude plugin install grillstorm@grillstorm
```

Run it with `/grillstorm:grillstorm`.

**Claude Code, as a personal skill**

```bash
git clone https://github.com/Lego1997/grillstorm
```

```bash
mkdir -p ~/.claude/skills && cp -r grillstorm/skills/grillstorm ~/.claude/skills/
```

Run it with `/grillstorm`.

**Cursor**

Copy `skills/grillstorm/` to `.cursor/skills/grillstorm/` in your project. Cursor also reads `~/.claude/skills/`, so the personal Claude Code install above covers both.

**Codex**

Copy `skills/grillstorm/` to `~/.agents/skills/grillstorm/` (older versions read `~/.codex/skills/`). Run it with `$grillstorm`.

**Other tools**

Any tool that reads Agent Skills can use the folder as is. In a tool without skills, paste the contents of `SKILL.md` as your first message and attach the two files in `assets/`.

## Use

Start it when you are about to begin a substantial deliverable:

> /grillstorm I need to write a policy brief on compute governance for our board next week.

The skill does not write the deliverable. It stops after handing you the plan and the prompt.

## Repo layout

```
.claude-plugin/          plugin and marketplace manifests for Claude Code
skills/grillstorm/
  SKILL.md               the workflow
  assets/
    plan-template.md     the plan.md the skill fills in
    init-prompt-template.md
  references/
    criteria-guide.md    how to write criteria an evaluator can apply
```

## Credits

Inspired by Matt Pocock's [grill-me skill](https://github.com/mattpocock/skills), which interviews you about a plan one question at a time, and by co-brainstorming with AI as a way of working.

## 中文简介

GrillStorm 是一个可在 Claude Code、Codex、Cursor 等工具中使用的 skill。它针对的问题是：结果可验证的工作（比如写代码、跑测试）很适合让模型循环迭代，但报告、备忘录、政策简报这类知识工作没有测试可跑，循环无从判断好坏。

GrillStorm 的做法是在动笔之前，先由模型和你一起讨论，产出一份 `plan.md`，其中包含：

1. 最终交付物的结构（严格使用 bullet points 和 sub-bullet points）
2. 成功标准：可由独立 sub-agent 逐条判定的二元检查项（必须引用原文作为证据），以及与你最满意的过往作品的并排比较

成功标准优先来自你自己满意的过往作品，其次是模型提出、由你逐条取舍的改进建议；两者都没有时，模型才会启动联网深度研究。

结束时你会得到一段 initialization prompt，可以贴到新的 session 或其他 AI 工具里，启动“起草、独立评估、修改”的循环。第一轮评估后会暂停一次请你确认，之后自动运行，直到全部通过或达到第 5 轮。

## Status

Version 0.1.0, first draft. No license has been chosen yet; one will be added before the repo is made public.
