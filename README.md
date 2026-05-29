# automate-my-workflow

A guided skill for [Claude Code](https://claude.ai/code) that runs a small-business owner or team lead through Codefi's **5-Step Workflow-to-AI Fit Check** — gate by gate — then hands qualified tasks to `skill-creator` or schedules a measurement loop. You end the session with installable skills or running measurement tasks, not a notebook full of ideas.

## Install

```bash
# Add the CodefiLabs marketplace (one-time)
/plugin marketplace add codefilabs/marketplace

# Install automate-my-workflow
/plugin install automate-my-workflow@codefilabs
```

## What it does

The skill activates whenever you ask things like "what should I automate", "where should I start with AI", "audit my workflows", or "AI fit check" — or when you describe recurring business tasks and want help deciding which deserve automation.

It walks five gated steps:

1. **List** your 10 most recurring tasks
2. **Mark** the tool and data behind each
3. **Classify** data sensitivity (Low / Medium / High)
4. **Rank** and pick by leverage (recurring, template-driven, low-sensitivity, time-consuming)
5. **Triage** each pick into *build skill now*, *measure first*, or *drop with reason*

Each step is a hard gate with an explicit override. Every session ends with artifacts — installable skills, scheduled measurement tasks, or a written record of what was deferred.

## Capability-aware

The skill detects what your runtime can do (file write, scheduled-tasks MCP, memory recall) and degrades gracefully — it never assumes a workspace folder, scheduling backend, or persistent memory.

## Source framework

Based on the Codefi blog "Before You Buy Another AI Tool, Map the Work That Actually Runs Your Business" (May 2026). The full framework and judgment rules ship in `skills/automate-my-workflow/references/blog-excerpts.md`.

## License

MIT
