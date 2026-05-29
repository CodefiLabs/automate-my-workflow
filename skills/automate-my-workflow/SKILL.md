---
name: automate-my-workflow
description: Run a small-business owner or team lead through the 5-Step Workflow-to-AI Fit Check from Codefi's "Before You Buy Another AI Tool" framework, gate-by-gate, then hand qualified tasks to skill-creator (or schedule a measurement loop) so the user ends the session with installable skills or running measurement tasks — not a notebook full of ideas. Use whenever the user asks "what should I automate", "where should I start with AI", "I want to use AI but don't know where", "audit my workflows", "map my recurring tasks", "automate my workflow", "AI fit check", "workflow fit check", "evaluate my work for AI", "which tasks should I automate first", "what work should I hand to AI", or describes recurring business tasks (invoicing, follow-ups, reporting, scheduling, expense categorization) and wants help figuring out which deserve automation. Also trigger when the user mentions they bought (or are considering) an AI tool and want to know what to point it at.
---

# automate-my-workflow

## What this does

Walks the user through Codefi's 5-Step Workflow-to-AI Fit Check from the blog "Before You Buy Another AI Tool, Map the Work That Actually Runs Your Business." Each step is a gate. Tasks that clear all gates get triaged into one of three paths: build a skill now (default), schedule a measurement loop first, or drop with a logged reason. The session ends with installable skills, scheduled measurement tasks, or both — never with a vague to-do list.

Full source framework lives at `references/blog-excerpts.md`. Load it when judgment calls are needed (Step 4 ranking, Step 5 triage).

## When to use

- User says "what should I automate" / "where should I start with AI" / "automate my workflow" / "AI fit check" / any phrase from the description above.
- User describes recurring business tasks and wants to know which to automate.
- User has bought (or is considering) an AI tool and needs to know what to point it at.
- User wants to re-audit their workflows after a quarter or after their work has changed.

## Operating principles

1. **One step at a time, gate by gate.** Batching the 5 steps collapses depth and breaks the gate logic. Always ask the current step's questions, wait for the answer, judge against the gate, then move on.
2. **Hard gates with explicit override.** When a gate fails, stop, explain WHY in specific terms (referencing the user's own answers), and offer the user the choice to continue anyway. Never silently override.
3. **Use the user's words.** Capture task names, tool names, and time estimates verbatim. Don't rename "follow up on overdue invoices" into "AR collections automation."
4. **Judge against the blog, not your training defaults.** When deciding "is this Low/Medium/High sensitivity" or "is this template-driven enough," reference `references/blog-excerpts.md`. The blog's rules are the source of truth.
5. **Capability-aware.** Detect what the runtime can do (file write, scheduled-tasks MCP, memory recall) and degrade gracefully. Never assume a workspace folder, a scheduling backend, or a persistent memory system.
6. **End with artifacts, not ideas.** Every session must produce either installable skills, scheduled measurement tasks, or a written "deferred to next month" record. No vague "here are some things you could think about."

## Pre-flight (before Step 1)

### 1. Detect capabilities silently
Check, in order, without narrating to the user:
- **File write to user's workspace?** Test by attempting to write a tiny file to a likely path (e.g., `~/Projects/_automate-my-workflow/.test`). If it works, persistence is available; remember the path.
- **Scheduled-tasks MCP available?** Look for `mcp__scheduled-tasks__*` tools. If present, the measurement-loop branch is unlocked.
- **Memory recall available?** Look for any `recall` / `memory` / `remember` tool. If present, attempt to recall prior `automate-my-workflow` sessions.

Record the three booleans (`canPersist`, `canSchedule`, `canRecall`) and use them silently throughout.

### 2. Auto-resume if prior state exists
If `canRecall` and a recall returns prior session state — OR if `canPersist` and a prior audit file exists — load it and open with:

> "Looks like you've run this before. Last time you qualified [N] tasks and built skills for [M]. Want to (a) pick up where we left off, (b) re-run the full audit fresh, or (c) build a skill from one of the qualified tasks you didn't pick last time?"

If nothing found, start fresh silently (no "I didn't find prior state" preamble).

### 3. One-line frame
Open the session with a single sentence that names what's about to happen:

> "I'll walk you through the 5-Step Workflow-to-AI Fit Check — five short questions. At the end, you'll have a list of tasks worth automating, and we'll build skills for the ones you pick."

Then ask Step 1.

## Step 1 — List your 10 most recurring tasks

Ask:

> "Name 10 things your team repeats every week or every month. Operational work that fills the hours — invoicing, follow-up emails, weekly reports, expense categorization, payroll runs, lead scoring, status updates, anything you do over and over."

Capture each one in the user's words. Number them 1-10.

### Gate
- **If user names 10 (or more):** continue to Step 2.
- **If user names fewer than 10:** STOP. Explain in specific terms:

> "You named [N] tasks. The framework calibrates on 10 because the gap between 'I can name 10' and 'I can only name 4' is usually a sign you haven't observed your own week closely enough yet — and AI tools don't fix that gap. The blog's recommendation is: observe your work for a week, write down what you actually do, then come back. **You can also override and continue with what you have** — just know the ranking will be thinner."

Offer two paths:
- (a) **Pause and observe.** If `canSchedule`, offer to create a daily 5pm "What did you actually do today?" reminder for 7 days. Otherwise tell them to add to a notes app daily for a week.
- (b) **Continue anyway.** Proceed to Step 2 with whatever count they gave, noting in the eventual summary that the audit ran with fewer than 10 tasks.

## Step 2 — Mark tools and data for each task

For each task captured in Step 1, ask:

> "For task #[N] '[task name]' — which tool does this run in (QuickBooks, HubSpot, Gmail, a spreadsheet, etc.), and what kind of data flows through it (customer names, dollar amounts, internal text, etc.)?"

Capture both per task. If user already mentioned the tool in Step 1, confirm it and ask only about the data.

### Gate
- This step doesn't fail — it produces data needed for Step 3. Move on once every task has a tool + data answer.
- If a task genuinely has no tool ("I just think about it"), flag it as non-automatable and exclude it from Step 3 onward (note in the eventual summary).

## Step 3 — Classify sensitivity per task

For each task, classify the data sensitivity using the blog's definitions:
- **Low:** Public information, non-sensitive operational data — marketing copy, scheduling, internal summaries.
- **Medium:** Business-specific data that could hurt if exposed — pricing formulas, pipeline details, vendor terms.
- **High:** Customer PII, financial records, employee data, HIPAA- or PCI-regulated information.

Propose your classification per task and confirm with the user:

> "For 'follow up on overdue invoices' running in QuickBooks with customer names, balances, and payment histories — I'd call that Medium (business-specific, could hurt if exposed). Agree, or move it?"

### Gate (per-task choice for High sensitivity)
For any task the user (or you) classifies as **High**, ask:

> "This is High sensitivity. Two choices: (a) drop this task from the audit and revisit when you have more guardrails in place, or (b) keep it in but commit to building with explicit guardrails (human-review-before-action, redaction of customer PII before AI sees it, etc.). Which?"

If the user faces 3+ High-sensitivity tasks in a row, offer a shortcut:

> "You've got several High items. Want to apply the same choice (drop or guardrails) to all remaining High tasks, or decide per-task?"

Mark each High task as either `dropped` or `guardrails-required` accordingly. Continue with all non-dropped tasks.

## Step 4 — Rank and pick

Take all tasks that survived Step 3 (Low, Medium, and High-with-guardrails). Rank them by the blog's criteria (load `references/blog-excerpts.md` if needed):

1. Recurring (weekly/monthly)
2. Template-driven (predictable structure)
3. Low-sensitivity (or guardrails committed)
4. Time-consuming enough to matter (>20 min per occurrence)

For each ranked task, ask any missing data (especially time estimate and template-driven-ness — these usually weren't captured yet):

> "For 'send weekly pipeline report' — roughly how long does it take you each time? And is the format pretty consistent each week, or does it vary a lot?"

Produce a ranked list, highest-leverage at top. Present it:

> "Here's your ranked list of [N] qualified tasks:
> 1. [task] — [tool], [sensitivity], ~[time]/run, [frequency], [template-driven?]
> 2. ...
> Which ones would you like to build now? You can pick one, several, or all. The blog recommends starting with one — but it's your call."

### Gate
- User must pick at least 1 to continue, OR pick 0 and the skill exits with the audit saved (if `canPersist`).

## Step 5 — Triage each picked task into build-now / measure-first / drop

For each task the user picked, ask:

> "For '[task]' — do you already know the rules and variance well enough to describe what 'correct' output looks like, or would you want to observe it a few more times before automating?"

Based on the answer + the rules in `references/blog-excerpts.md`, route to one of:

### Path A: Build skill now (default)
If the user can describe the task clearly and it meets the build-now criteria, proceed to skill creation:
- **If skill-creator is available as an invokable skill:** invoke it, passing the task name, tool, data, sensitivity, frequency, time estimate, and any guardrails. Skill-creator will ask clarifying questions and produce the SKILL.md.
- **If skill-creator is not available:** walk the user through the skill-creator protocol inline (yaml frontmatter, description with triggers, operating principles, output shape). Save the resulting SKILL.md to `~/Projects/_skills/<task-slug>/SKILL.md` if `canPersist`, otherwise output it inline for the user to save manually.

### Path B: Schedule a measurement task first
Only available if `canSchedule`. If the user wants to observe before automating:
- Create a scheduled task at appropriate cadence (matches the task's natural cadence — weekly task → weekly reminder).
- Reminder prompt: "Did you run '[task]' this week? If yes, how long did it take, what was hard, and would AI have helped?"
- State file at `~/Projects/_automate-my-workflow/measurements/<task-slug>/state.yaml` (if `canPersist`) with threshold (default: 3 logged runs) and current count.
- Append log at `~/Projects/_automate-my-workflow/measurements/<task-slug>/measurements.md`.
- At threshold, the scheduled task can re-invoke `automate-my-workflow` with the measurement data, which triggers Path A for that task.

### Path C: Drop with reason
If the user decides not to build or measure, capture the reason and add to the deferred list.

## Sunset offers (after Path A completes for a measurement-derived task)

If a skill was just created from a task that came out of Path B (had a measurement loop running), offer:

> "You built the skill from the measurement data. Want me to turn off the scheduled measurement task for '[task]' so it stops nagging you?"

Default to yes unless the user wants to keep measuring.

## End-of-session summary

When all picked tasks have been routed, produce the final summary. Always include all four sections, even if empty:

```
## Workflow Audit Summary — [YYYY-MM-DD]

### Skills built ([N])
- [skill-name] — [task] — [path if saved]
- ...

### Measurement tasks scheduled ([N])
- [task] — [cadence] — [threshold: N runs] — [state file path if saved]
- ...

### Deferred / dropped ([N])
- [task] — [reason: "user wants more observation" / "High sensitivity, user dropped" / "not a fit"]
- ...

### What to do next
- [Run skills 2-3 times this week, then come back and tell me what worked]
- [Wait for measurement tasks to hit threshold — I'll surface them]
- [Re-run `automate-my-workflow` next month or when your work changes shape]
```

If `canPersist`, save this summary to `~/Projects/_automate-my-workflow/audits/<YYYY-MM-DD>-audit.md`. If `canRecall`, also store a one-line pointer in memory ("Completed audit YYYY-MM-DD; built N skills; M in measurement; K deferred").

## Edge cases

- **User picks 0 tasks at Step 4:** save the audit if possible, suggest re-running in a month, end gracefully.
- **All tasks are High sensitivity and user drops them all:** end with "Looks like your week is mostly handling sensitive data right now. The framework recommends building observation muscle first — would you like to re-run this audit next quarter when you've added safer tasks to compare against?"
- **User quits mid-flow:** if `canPersist`, save partial state so resume works next time.
- **User says they have ZERO recurring tasks:** they're not the audience for this skill. Suggest they revisit when their week settles into a pattern.

## Pairing with other skills

- **skill-creator** — Path A's default delivery mechanism. Hand off task spec; skill-creator handles SKILL.md scaffolding.
- **run-workflow / `_workflows/`** — for tasks that need orchestration across multiple AI steps, the resulting "skill" might better be a workflow file. Surface this option when the user describes a multi-step pipeline.
- **scheduled-tasks** — Path B's measurement loop and Step 1's observation reminders.

## Honest limitations

- Doesn't currently check Colorado SB 26-189 or other jurisdiction-specific AI consequential-decision rules. If the user mentions hiring screens, credit decisions, insurance, or housing — flag manually and recommend they consult counsel before automating.
- Doesn't audit existing automation. If the user already has Zapier / n8n / SaaS-native automations, mention this skill won't deduplicate against them.
- The 20-minute saving threshold and 10-task floor are heuristics from the blog. They calibrate well for small-business owners; for solo creators or large teams, the user may need to mentally adjust.

## References

- `references/blog-excerpts.md` — full source framework + judgment rules. Load when ranking tasks or making triage calls.
- Source blog: "Before You Buy Another AI Tool, Map the Work That Actually Runs Your Business" (Codefi, May 2026).
