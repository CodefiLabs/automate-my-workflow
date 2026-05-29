# automate-my-workflow

A guided skill for [Claude Code](https://claude.ai/code) that runs a small-business owner or team lead through Codefi's [**5-Step Workflow-to-AI Fit Check**](https://codefiworks.com/ai-insights/map-first-automate-second-ai-fit-check) — gate by gate — then hands qualified tasks to `skill-creator` or schedules a measurement loop. You end the session with installable skills or running measurement tasks, not a notebook full of ideas.

## Install (Claude desktop app — free, no terminal)

These steps are for the **Claude desktop app**, the easiest way to use this if you're not a developer. **A free Claude account works** — you don't need a paid plan and you never touch a terminal.

### 1. Get the Claude desktop app

Download and install the free Claude desktop app, then open it and **sign in**:

- **Mac:** https://claude.ai/api/desktop/darwin/universal/dmg/latest/redirect
- **Windows:** https://claude.ai/api/desktop/win32/x64/setup/latest/redirect

### 2. Open Cowork → Customize

1. In the app, open the **Cowork** tab.
2. Go to the **Customize** page. In the left sidebar you'll see **Skills**, **Connectors**, and a **Personal plugins** section.

### 3. Add the plugin (two ways — pick one)

**Easiest — download and upload the file:**

1. [**Download `automate-my-workflow.zip`**](https://github.com/CodefiLabs/automate-my-workflow/releases/latest/download/automate-my-workflow.zip) (downloads instantly when you click it).
2. Next to **Personal plugins**, click the **+** button → **Create plugin** → **Upload plugin**, and choose the `automate-my-workflow.zip` file you just downloaded.

**Or — add the CodefiLabs marketplace** (this also gets you future updates and other CodefiLabs plugins):

1. Next to **Personal plugins**, click the **+** button → **Create plugin** → **Add marketplace**, then enter and confirm:

   ```
   codefilabs/marketplace
   ```

2. Click the **+** again → **Browse plugins**, find **automate-my-workflow** in the list, and click to install it.

Either way, the skill is now active.

### 4. Use it

Just talk to Claude in plain English — for example:

> *"Help me figure out what parts of my business I should automate."*

Claude will start the 5-Step Fit Check and walk you through it one question at a time.

---

<details>
<summary>Developers: install from the terminal (Claude Code CLI) instead</summary>

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

Based on the Codefi article [**Map First, Automate Second: The AI Fit Check**](https://codefiworks.com/ai-insights/map-first-automate-second-ai-fit-check). The full framework and judgment rules ship in `skills/automate-my-workflow/references/blog-excerpts.md`.

## License

MIT
