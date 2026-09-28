---
name: eds-readiness
description: One-time environment setup before building AEM Edge Delivery (EDS) demos — checks git/Node/AEM CLI, guides creating a GitHub account, and confirms readiness, then recommends the next step. Use when someone says "get me set up", "readiness check", "set up my machine for EDS demos", "am I ready to build a demo", or is starting EDS demo work for the first time.
---

# EDS Demo Readiness

Guide an Adobe XSC product specialist — possibly non-technical — so their machine and accounts are ready to build
AEM Edge Delivery demos. This is **setup only**; building a demo is the `create-eds-repo` skill.

## How to run this

- **MANDATORY — ask with clickable dialogs.** You MUST call the AskUserQuestion tool for these and NEVER present a numbered/bulleted prose option list. Whenever you need input or a choice from the user, ask via a clickable
  AskUserQuestion dialog — use the free-text box for open answers (like a site name) and options for choices —
  instead of prose questions.
- Adapt to your environment: if you have terminal/file tools, run the version checks yourself and report ✅ / ❌.
  If you can't run commands, ask the user to run each and paste the output, then interpret it. Give the fix for
  anything missing.
- Go one section at a time and confirm before moving on. Keep language plain.
- The user creates their own GitHub account themselves — you guide, you don't do it for them. Never ask the user to
  paste passwords or tokens into chat.
- At the end, give a short ✅ readiness summary, then recommend the next skill based on intent (see step 4).

## 1. Check local tools

Run these and report ✅ / ❌ for each:
```bash
git --version
node --version
aem --version
```
Install anything missing:
- **Node.js** (includes npm) — LTS from https://nodejs.org
- **git** — https://git-scm.com
- **AEM CLI**: `sudo npm install -g @adobe/aem-cli`

## 2. GitHub Enterprise account

All XSC demos must use **GitHub Enterprise** accounts.

**Ask the user (via AskUserQuestion with three options):** Do you have a GitHub Enterprise account?

- **Yes** — Confirm it's active and ready to use.
- **No** — Direct them to set up a new account:
  → **https://github-copilot.corp.adobe.com/getting-started**
  
  Follow the setup wizard to:
  1. Create your GitHub Enterprise account (use your Adobe email)
  2. Verify and activate your account
  3. Set up your profile
  
  Your demo repos will live under your Enterprise account org.

- **I don't know, can I check?** — Open the GitHub Enterprise SSO login so they can verify:
  → **https://github.com/enterprises/adobe-prd/sso**
  
  They can log in with their Adobe credentials to check if they already have access. If they log in successfully, they have an account. If not, they'll need to create one at the getting-started link above.

## 3. Connect the AEM DA content tools (recommended)

Connect the **AEM DA** MCP so Claude can read and seed **Document Authoring** content directly — e.g. copy default
content into a new demo, or seed a blank site — without manual browser steps.

- Server: **AEM DA - Prod** → `https://mcp.adobeaemcloud.com/adobe/mcp/da`
- Authenticate it via your **claude.ai connector settings** (or `/mcp` in an interactive Claude Code terminal).
  Claude can't run the sign-in flow for the user — direct them to do it.
- When it shows **connected**, the `da_*` tools (list / copy / create content) become available.

Optional but recommended: without it, content seeding falls back to the browser (`da.live`).

> **If the DA MCP is failing** (tools erroring, "server disconnected", or `da_*` calls hang): have the user
> **disconnect the AEM DA connector and reconnect it** — in their claude.ai connector settings (or `/mcp` in an
> interactive terminal) — then retry. A stale/expired connection is the usual cause.

## 4. Readiness check & next step

Confirm and summarize as a ✅ checklist:
- git, Node, and the AEM CLI are installed.
- A GitHub Enterprise account is created and ready.
- *(Recommended)* the AEM DA MCP is connected (for content seeding).

Then ask what the user wants to do next and recommend:
- **"I just want to build a demo"** (most people) → the **`create-eds-repo`** skill.
- **"I want my own reusable base template first"** → the **`create-base-template`** skill (one-time), then
  `create-eds-repo` for each demo.

> Rule of thumb: if unsure, go straight to `create-eds-repo` — you can always make a base template later.

## Reference links

| Resource | Link |
|---|---|
| GitHub Enterprise Setup | https://github-copilot.corp.adobe.com/getting-started |
| GitHub Enterprise SSO Login | https://github.com/enterprises/adobe-prd/sso |
| Node.js | https://nodejs.org |
| AEM CLI (npm) | `@adobe/aem-cli` |
