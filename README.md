# automate-my-workflow

A guided skill for [Claude Code](https://claude.ai/code) that runs a small-business owner or team lead through Codefi's **5-Step Workflow-to-AI Fit Check** — gate by gate — then hands qualified tasks to `skill-creator` or schedules a measurement loop. You end the session with installable skills or running measurement tasks, not a notebook full of ideas.

## Install (Claude desktop app — no terminal needed)

These steps are written for the **Claude desktop app**, the easiest way to use this if you're not a developer. You'll paste two short commands once, then click to install.

### 1. Get the Claude desktop app

Download and install the free Claude desktop app for your computer:

- **Mac:** https://claude.ai/api/desktop/darwin/universal/dmg/latest/redirect
- **Windows:** https://claude.ai/api/desktop/win32/x64/setup/latest/redirect

Open the app and **sign in** with your Anthropic (Claude) account.

> **You'll need a paid plan** (Pro, Max, Team, or Enterprise) to use the coding features. The free plan won't show the **Code** tab. You can subscribe at https://claude.com/pricing.

### 2. Open the Code tab

1. At the top of the app, click the **Code** tab.
2. Choose **Local**, click **Select folder**, and pick any folder on your computer (it can be an empty one — it's just a workspace).
3. You'll now see a text box where you type messages to Claude. That's where the next two steps go.

### 3. Add the CodefiLabs marketplace (one time)

Click into the message box, type the line below exactly, and press Enter:

```
/plugin marketplace add codefilabs/marketplace
```

This tells Claude where to find CodefiLabs plugins. You only ever do this once.

### 4. Install the plugin

Now you have two ways to finish — pick whichever feels easier:

**Option A — point and click:** Click the **+** button next to the message box → choose **Plugins** → **Add plugin**. Find **automate-my-workflow** in the list and click to install it. Choose **User** scope so it works in every folder.

**Option B — type one more command:** In the message box, type and press Enter:

```
/plugin install automate-my-workflow@codefilabs
```

That's it. The skill is now active.

### 5. Use it

Just talk to Claude in plain English — for example, type:

> *"Help me figure out what parts of my business I should automate."*

Claude will start the 5-Step Fit Check and walk you through it one question at a time.

---

<details>
<summary>Using the terminal (Claude Code CLI) instead?</summary>

```bash
# Add the CodefiLabs marketplace (one-time)
/plugin marketplace add codefilabs/marketplace

# Install automate-my-workflow
/plugin install automate-my-workflow@codefilabs
```

</details>

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
