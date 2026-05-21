# 🏭 The n8n Factory

**Use Claude Code to brainstorm, plan, build, and enhance [n8n](https://n8n.io) workflows — automatically.**

This project turns Claude Code into a team of expert n8n developers that work for you 24/7. You describe what you want in plain English; the Factory designs it, builds it directly in your n8n account, and teaches you how to use it.

You don't need to know how to code. You act as the **Product Owner**: you provide the vision, you supply your account passwords (credentials), and you do the final testing. The Factory does the building.

---

## What's in the box

When you copy this project, you already get everything the Factory needs:

| Piece | What it does |
|-------|--------------|
| **`CLAUDE.md`** | A permanent "brain chip" that tells Claude exactly how to behave as an n8n expert. |
| **`.claude/skills/`** | A library of 7 deep-expertise guides for n8n logic, expressions, and code. |
| **`.mcp.json`** | The connector that lets Claude reach out and build workflows in *your* n8n account. |
| **Numbered folders** | A simple `1-inputs` → `2-brainstorm` → `3-plan` → `4-workflows` assembly line. |

Because all of that ships inside this project, your setup is short: **make your own copy, open it in the cloud, install Claude Code, and connect your n8n account.** That's it.

---

## How it works

The Factory is a small stack of layers working together:

1. **The Studio** — [GitHub Codespaces](https://github.com/features/codespaces) gives you a free, secure, cloud-based computer ("VS Code") to work in. Nothing is installed on your own machine and nothing on your machine is at risk.
2. **The Brain** — **Claude Code** is a special version of Claude that can read files, run tools, and build things — not just chat.
3. **The Expertise** — `CLAUDE.md` and the `.claude/skills/` folder make Claude behave like a senior n8n developer.
4. **The Connector** — the **n8n MCP** server lets Claude talk directly to your n8n account to create, fix, and run workflows.
5. **The Engine** — your **n8n instance**, where the finished automations actually run.

**The loop:** You give an instruction → Claude reads its skills and best practices → Claude builds the workflow in your n8n account → you add credentials and test.

---

## What you'll need before starting

- A computer with internet access and a web browser
- An email address
- About **30–45 minutes**
- A **Claude account** — Pro ($20/mo) or Max ($100–200/mo) — sign up at [claude.ai](https://claude.ai)
- A **paid n8n account** — required, because the free plan can't create the API key the Factory needs. Get one at [n8n.io](https://n8n.io) (cloud) — any paid tier works.

You do **not** need a GitHub account yet — we'll create one in Part 1.

---

# Setup

## Part 1 — Create a GitHub account

GitHub is where this project lives. It's free.

1. Open your web browser and go to **[github.com](https://github.com)**.
2. Click **Sign up** in the top-right corner.
3. Enter your email address, create a strong password, and choose a username.
4. Complete the verification puzzle, then enter the code GitHub emails you.

✅ You now have a GitHub account.

## Part 2 — Make your own copy of the Factory

This project is a **template**. You'll create your own private copy to work in.

1. Go to the n8n Factory repository page on GitHub (the link you were given to get here).
2. Click the green **Use this template** button near the top-right.
3. Choose **Create a new repository**.
4. Give it a name (for example, `my-n8n-factory`).
5. Choose **Private** (recommended — your n8n key will live inside).
6. Click **Create repository**.

✅ You now have your own copy of the Factory. Everything from here happens in *your* copy.

## Part 3 — Open it in a Codespace

A **Codespace** is a complete computer that runs in your browser. No installing anything.

1. On your new repository's page, click the green **Code** button.
2. Click the **Codespaces** tab.
3. Click **Create codespace on main**.
4. Wait 1–2 minutes while it builds.

When it loads you'll see **VS Code** — a code editor — with three areas:

- **Left:** the File Explorer (your project files)
- **Middle:** the Editor (where files open)
- **Bottom:** the Terminal (you'll barely touch it)

> 💡 To preview any `.md` file (like this one) as nice formatted text, open it and press **Ctrl+Shift+V** (Windows) or **Cmd+Shift+V** (Mac).

## Part 4 — Install Claude Code

There are two ways to run Claude Code. **Pick one:**

- **Part 4a — VS Code Extension** — point-and-click, easiest. *Recommended for beginners.*
- **Part 4b — Terminal** — runs in the bottom Terminal panel, with handy `dsp` shortcuts.

Both work exactly the same for building workflows. If you're not sure, use **4a**.

### Part 4a — VS Code Extension (recommended)

1. In the left sidebar, click the **Extensions** icon (four squares, one flying off).
2. In the search box, type **Claude Code**.
3. On the official **Claude Code** extension (by Anthropic), click **Install**.
4. When it finishes, the Claude panel opens. Click **Sign in** and log in with your Claude account (the Pro or Max account from the requirements).
5. When asked how Claude should handle file changes, choose **Accept Edits** (also called *Auto-accept edits*). This lets the Factory work smoothly without asking permission for every small change.

✅ Claude Code is now running. **Skip Part 4b** and go to [Part 5](#part-5--connect-your-n8n-account).

### Part 4b — Terminal (with `dsp` shortcuts)

Prefer the terminal? Here's the setup.

**1. Open the Terminal.** It's the panel along the bottom of your Codespace — click the **Terminal** tab. *(Don't see it? Press `Ctrl` + `` ` `` — the backtick key, next to the `1`.)*

**2. Install Claude Code.** Paste this line into the terminal and press Enter, then wait 1–2 minutes:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**3. Create the `dsp` shortcuts.** By default Claude Code asks permission before almost every action, which is slow for automation. These two shortcuts launch it in "skip permissions" mode so the Factory runs smoothly. Paste this single line and press Enter:

```bash
echo -e "alias dsp='claude --dangerously-skip-permissions'\nalias dsp-c='claude --dangerously-skip-permissions -c'" >> ~/.bashrc
```

Then load the shortcuts:

```bash
source ~/.bashrc
```

You now have two commands:
- **`dsp`** — start Claude Code (skipping permission prompts)
- **`dsp-c`** — start Claude Code and continue your last conversation

> ⚠️ **Safety note.** "Skip permissions" lets Claude run commands without asking first. That's fine **here** — a private Codespace is a safe, throwaway environment. Only use this mode in environments you trust.

**4. Start and sign in.** Type `dsp` and press Enter. The first time:
- Choose **1** to sign in with your Claude Pro/Max account.
- Open the link it shows, click **Authorize**, and paste the key back into the terminal. *(If authorizing fails the first time, open the link again and retry — a known hiccup.)*

✅ Claude Code is now running in your terminal.

## Part 5 — Connect your n8n account

The Factory needs two things from your n8n account: your **instance URL** and an **API key**.

> 💡 **Need a paid n8n plan?** A paid plan is required for the API key. **[Upgrade your n8n account through this link](https://n8n.partnerlinks.io/p2xklomu2gq2)** to get extra credits.

**Get them from n8n:**
- **Instance URL** — the web address of your n8n, e.g. `https://your-name.app.n8n.cloud`
- **API key** — in n8n, go to **Settings → n8n API → Create an API key**, then copy it. *(This is why a paid n8n plan is required — free plans can't create API keys.)*

**Put them into the Factory.** In the Claude Code chat panel, paste this prompt:

> **Copy `.mcp.json.example` to a new file called `.mcp.json`, then ask me for my n8n URL and API key and fill them in.**

Claude will create the file and ask you for the two values. Paste them in when prompted.

> 🔒 **Your key stays private.** `.mcp.json` is listed in `.gitignore`, so your API key is never uploaded to GitHub. (Prefer to do it by hand? Open `.mcp.json.example`, copy it to `.mcp.json`, and replace the two placeholder values yourself.)

## Part 6 — Start a fresh session and verify it worked

The connector only loads when a Claude Code session starts, so start a new one:

- **Extension (4a):** click the **+** (New session) button at the top of the Claude Code panel.
- **Terminal (4b):** type `exit` to close Claude Code, then run `dsp` again.

The new session loads the connection from `.mcp.json`.

Now **test the connection for real.** In Claude Code, ask:

> **What n8n workflows do I have?**

- ✅ If Claude lists your workflows (or says you have none yet), the connection works — you're ready.
- ❌ If Claude says it can't access n8n, see [Troubleshooting](#troubleshooting) below.

> ⚠️ **Don't trust a "Connected" badge alone.** The connector always shows as "connected" even with a wrong key — the *only* reliable test is asking Claude to actually list your workflows.

---

# Using your Factory

This is the fun part. The Factory works as a 4-step assembly line, and the numbered folders match the steps. **You drive it entirely by chatting with Claude Code** — just type the prompts below.

```
1-inputs  →  2-brainstorm  →  3-plan  →  4-workflows  →  (your live n8n account)
 tell it      get ideas       design     build it &
 about you                    the build  guide you
```

## Step 1 — Tell the Factory about your business 📋

Great automation ideas depend on knowing *your* business. The `1-inputs/` folder holds two fill-in forms:

- **[1-inputs/about.md](1-inputs/about.md)** — what your business *is*: what you do, your customers, your brand voice.
- **[1-inputs/tech-stack.md](1-inputs/tech-stack.md)** — what your business *uses*: your role, your departments, your tools, your biggest time-wasters.

The fastest way to fill in `about.md` is to let Claude interview you starting from your website. Paste this prompt:

> **Look at our website https://your-company.com and interview me one question at a time to fill in `1-inputs/about.md`.**

Then do the same for your tools:

> **Interview me one question at a time and fill in `1-inputs/tech-stack.md` with my answers.**

You can also **fill either file in yourself**, or **drop your own documents into the `1-inputs/` folder** for extra context — brand guidelines, a pitch deck, an existing About page, product sheets. (To upload a file, drag it from your computer into the `1-inputs/` folder in the VS Code Explorer on the left.) The Factory reads everything in `1-inputs/`.

Do this once. Everything the Factory builds from now on is tailored to what's in this folder.

## Step 2 — Brainstorm workflow ideas 💡

Ask the Factory for ideas. Here are prompts for different approaches — try whichever fits:

- **Tailored to your business:**
  > Based on `1-inputs/tech-stack.md`, give me 10 n8n workflow ideas that would save my team the most time. Save them to `2-brainstorm/`.
- **For one department:**
  > Brainstorm 5 n8n workflows for my marketing team and save them to `2-brainstorm/marketing-ideas.md`.
- **From scratch / popular ideas:**
  > What are the most popular n8n workflows for a business like mine? Save the list to `2-brainstorm/`.
- **Your own idea — get a second opinion:**
  > Here's an idea: every time a customer fills out our contact form, log them in our spreadsheet and send a welcome email. Is this a good fit for n8n? Save your assessment to `2-brainstorm/`.

Claude saves each brainstorm into the [2-brainstorm/](2-brainstorm/) folder so you can review and compare.

## Step 3 — Turn one idea into a plan 📐

Pick the idea you like best and ask Claude to design it properly:

> **Take the lead-welcome idea from `2-brainstorm/` and create a detailed plan for an n8n workflow. Save it to `3-plan/`.**

Claude writes a full specification — every step, every node, what connects to what, and which of *your* tools it touches — into the [3-plan/](3-plan/) folder. Review it. If something's off, just say so:

> Change the plan so it also adds the customer to our CRM.

## Step 4 — Build it and learn to use it 🔨

When the plan looks right, tell the Factory to build it for real:

> **Use the n8n skills to build the workflow from `3-plan/` in my n8n instance, then guide me on how to use it.**

Claude will design, validate, and create the workflow directly in your n8n account, then save a plain-English usage guide into [4-workflows/](4-workflows/).

## Step 5 — Add your credentials and test ✅

The Factory builds the *structure* of the workflow, but it can't log into your private accounts for you. The last step is yours:

1. Open your n8n instance in a browser and find the new workflow.
2. Open any node that connects to a service (Gmail, Slack, your CRM…). n8n will ask you to **add a credential** — sign in to that service once and n8n remembers it.
3. Use n8n's **Test workflow** button to run it.
4. When it works, toggle the workflow to **Active**.

Stuck on a step? Ask Claude — it can walk you through adding a specific credential.

## Keep improving (the enhance loop) ♻️

The Factory doesn't stop at "built." Come back any time:

- **Fix something broken:** *"This workflow failed with this error: [paste error]. Find the problem and fix it."*
- **Add a feature:** *"Add a step to that workflow that also posts a message to our Slack #sales channel."*
- **Understand it:** *"Explain what my 'Daily Report' workflow does, step by step."*

---

## The skills behind the Factory

Inside [.claude/skills/](.claude/skills/) are 7 expert guides. **You never call these yourself** — Claude loads the right one automatically at the right moment. They're listed here so you know what's powering the Factory:

| Skill | Powers this step | What it knows |
|-------|-----------------|---------------|
| `n8n-workflow-patterns` | Plan (3) | Proven workflow blueprints — webhooks, AI agents, scheduled jobs, batch jobs. |
| `n8n-mcp-tools-expert` | Build (4) | How to search nodes, validate, and deploy into your n8n account correctly. |
| `n8n-node-configuration` | Build (4) | How to set up each node's settings so it works the first time. |
| `n8n-expression-syntax` | Build (4) | How to pass data correctly between steps (the #1 source of errors). |
| `n8n-validation-expert` | Build (4) | How to read validation errors and tell real problems from false alarms. |
| `n8n-code-javascript` | Build (4) | Writing JavaScript for the occasional custom step. |
| `n8n-code-python` | Build (4) | Writing Python for the occasional custom step. |

---

## Project structure

```
my-n8n-factory/
├── README.md            ← you are here
├── CLAUDE.md            ← Claude's permanent instructions (don't edit)
├── .mcp.json            ← your private n8n connection (never uploaded)
├── .mcp.json.example    ← the template for the file above
├── .claude/skills/      ← the 7 expert skills
├── 1-inputs/            ← about.md + tech-stack.md (+ any context you add)
├── 2-brainstorm/        ← workflow ideas land here
├── 3-plan/              ← detailed workflow designs land here
└── 4-workflows/         ← built workflows + how-to-use guides land here
```

---

## Example prompts

Things you can ask the Factory any time:

- *"Explain to me what this is and how to use it."*
- *"Build a workflow that emails me an AI-generated news summary every morning at 6:00 AM."*
- *"Review `1-inputs/tech-stack.md` and give me 5 workflow ideas that would increase my profit."*
- *"What n8n workflows do I already have?"*
- *"Turn this idea into a full specification: [your idea]."*
- *"Now build that workflow in my n8n instance and tell me how to use it."*
- *"My 'Invoice Reminder' workflow stopped working — investigate and fix it."*

---

## Troubleshooting

**Claude can't see my n8n workflows / says it can't access n8n.**
1. Check that `.mcp.json` exists (not just `.mcp.json.example`) and that both the URL and API key are filled in with no quotes missing.
2. The URL should have no trailing slash and look like `https://your-name.app.n8n.cloud`.
3. API keys expire. If yours is old, create a fresh one in n8n (**Settings → n8n API**) and update `.mcp.json`.
4. After any change to `.mcp.json`, start a **new Claude Code session** — extension: the **+** button; terminal: `exit` then `dsp` again. Changes only take effect in a fresh session.
5. Re-test by asking *"What n8n workflows do I have?"* — never rely on a "Connected" badge.

**A workflow runs but a step fails.**
Copy the error message from n8n and paste it to Claude: *"This step failed with: [error]. Fix it."*

**A node says "credentials required."**
That's normal — the Factory can't log into your accounts. Open that node in n8n and add the credential yourself (Step 5 above). Ask Claude if you need a walkthrough.

---

## Resources

- **n8n documentation:** [docs.n8n.io](https://docs.n8n.io)
- **Claude Code documentation:** [docs.claude.com/en/docs/claude-code](https://docs.claude.com/en/docs/claude-code)
- **GitHub help:** [docs.github.com](https://docs.github.com)

Happy automating! 🚀
