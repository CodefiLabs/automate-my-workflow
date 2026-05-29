# Blog Excerpts — Source Material for `automate-my-workflow`

Source: "Before You Buy Another AI Tool, Map the Work That Actually Runs Your Business" (Codefi blog draft, May 2026). These passages are the load-bearing framework the skill uses to judge candidate tasks. Quote verbatim where shown; paraphrase only where labeled.

---

## The 5-Step Workflow-to-AI Fit Check (full framework)

### Step 1 — List your 10 most recurring tasks
> "Write down ten tasks your team repeats every week or month. Not goals. Not projects. The operational work that fills the hours: invoicing, payroll reporting, follow-up emails, lead scoring, month-end close, campaign posting, client status updates, expense categorization, inventory reorders, compliance filing."

**Gate condition (verbatim):**
> "If you cannot list ten, you are not ready to evaluate AI tools — you are ready to observe your own work for one week. Write down what you actually do."

### Step 2 — Mark the tools and data each task touches
> "For each task, note which platform it runs on and what data flows through it."

> "Example: 'Follow up on overdue invoices' runs in QuickBooks, touches customer names, balances, and payment histories. 'Send weekly pipeline report' runs in HubSpot, touches deal stages, contact details, and revenue forecasts."

> "This step is short but critical. It makes your data landscape visible before any AI tool touches it."

### Step 3 — Classify sensitivity (Low / Medium / High)

> "Rate the data sensitivity of each task:
> - Low: Public information, non-sensitive operational data — marketing copy, scheduling, internal summaries.
> - Medium: Business-specific data that could hurt if exposed — pricing formulas, pipeline details, vendor terms.
> - High: Customer PII, financial records, employee data, HIPAA- or PCI-regulated information."

### Step 4 — Pick one low-risk, high-frequency task
> "Do not automate your most critical workflow first. Pick the task that scores Low on sensitivity and High on frequency. A weekly summary, a draft report, a recurring data formatting step — something that eats time but would not damage your business if an AI model generated an imperfect version."

> "The goal is a controlled experiment, not a bet-the-business rollout."

### Step 5 — Test on a draft first, then measure
> "Run the AI output as a draft or recommendation — not as autonomous action. A human reviews before anything ships, sends, or posts. Then measure:
> - How much time did the draft save?
> - How many corrections did the reviewer make?
> - Would you run this task again with AI next week?"

> "If the answer to the last question is yes, you have your first validated AI workflow. If not, you learned something without risking data or reputation."

---

## What to automate first (Step 5 + Step 4 ranking criteria)

> "Start with tasks that are:
> - Recurring (you do them weekly or monthly)
> - Template-driven (they follow a predictable structure)
> - Low-sensitivity (a draft output does not expose customer or financial data)
> - Time-consuming enough to matter (saving 20 minutes on a weekly task is real; saving 2 minutes is not)"

## What to leave alone for now

> "Leave alone for now:
> - High-sensitivity decisions — hiring screens, credit decisions, insurance quotes, anything that affects people's access to housing, employment, lending, or insurance.
> - Customer-facing communications without human review — AI-generated copy should always pass through a person who represents your brand.
> - Compliance-bound processes — until you have tested AI on low-risk drafts, do not let it touch regulated workflows."

---

## Distilled judgment rules (for skill use)

These are the rules the agent applies when triaging a qualified task into "build skill now" vs "schedule a measurement task first" vs "drop":

1. **Build skill now** when:
   - User can describe the task's rules + variance clearly
   - Task is template-driven (predictable structure)
   - Saving > 20 minutes per occurrence OR runs at least weekly
   - Sensitivity is Low (or Medium with explicit guardrails the user names)

2. **Schedule a measurement task first** when:
   - Task is recurring but the user can't yet name the variance pattern
   - The time-eating claim hasn't been validated (might save 20 min — or might save 2)
   - Task is in scope but the user wants observation before committing

3. **Drop (with reason logged)** when:
   - High sensitivity AND user does not want to build with guardrails
   - Task is a one-off, not recurring (fails the framework before triage)
   - Task affects people's access to housing, employment, lending, or insurance — and the user is uncomfortable taking the safety burden

4. **Always include human-in-the-loop draft review** in any built skill or measurement task. Never deliver autonomous action on the first pass.

---

## Saving threshold definition

> "Saving 20 minutes on a weekly task is real; saving 2 minutes is not."

Use **20 minutes per occurrence** as the practical lower bound for "time-consuming enough to matter." If the user can't estimate, ask. If they say "it varies," default the task to a measurement-first path.

---

## Frequency definition

Recurring = the user does it weekly or monthly. Daily counts too, but skill should flag daily tasks as the highest-value targets (highest cumulative time savings).
