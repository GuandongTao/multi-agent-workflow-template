# AI-Native Project Template

A reusable project template for a lightweight solo AI development workflow:

**Brainstorm in Claude → maintain project memory in Obsidian → formalize approved work with Spec Kit → plan/review with Claude Code → optionally delegate implementation to Codex → version everything in Git/GitHub.**

The goal is to keep product thinking, implementation specs, and code connected without turning the workflow into a heavy process.

---

## What this template is for

This setup separates project knowledge into three layers:

- **Obsidian (`brain/`)** — evolving product/system understanding, features, decisions, open questions, and a visual Canvas.
- **Spec Kit** — approved requirements, implementation plans, tasks, and consistency checks.
- **Git/GitHub** — code, history, pull requests, and CI.

Claude Project is used for brainstorming and ongoing project-memory maintenance. Claude Code is used for planning/review and can optionally delegate implementation through MCP to Codex.

---

## Suggested repository structure

```text
your-project/
├─ brain/
│  ├─ PROJECT.md
│  ├─ PROJECT.canvas
│  ├─ Features/
│  ├─ Decisions/
│  └─ .obsidian/
├─ specs/
├─ src/
├─ tests/
├─ .github/
├─ setup/
│  └─ CLAUDE_PROJECT_INSTRUCTIONS.md
├─ AGENTS.md
├─ CLAUDE.md
├─ .gitignore
└─ README.md
```

`brain/` is the Obsidian vault root. The entire code repository does **not** need to be an Obsidian vault.

---

## 1. Prerequisites

Install the tools you want to use:

- Git
- GitHub account
- Obsidian
- Claude Desktop
- Claude Code
- Optional: Codex CLI
- Optional: GitHub Spec Kit
- VS Code or another editor

This template does not include API keys, bearer tokens, local paths, or other machine-specific credentials.

---

## 2. Create a project from this template

On GitHub:

1. Open this template repository.
2. Click **Use this template**.
3. Choose **Create a new repository**.
4. Give the new repository a name.
5. Clone it locally.

GitHub template repositories create a new repository with the template's files and structure but with independent Git history.

---

## 3. Open the project brain in Obsidian

Open:

```text
<repo>/brain
```

as an Obsidian vault.

Expected starter structure:

```text
brain/
├─ PROJECT.md
├─ PROJECT.canvas
├─ Features/
└─ Decisions/
```

Keep `PROJECT.md` concise. `PROJECT.canvas` is the visual project map.

---

## 4. Install the Obsidian MCP Connector

In Obsidian:

1. Open **Settings → Community plugins → Browse**.
2. Search for **MCP Connector** by `istefox`.
3. Install and enable it.
4. Open **Settings → MCP Connector → Access control**.
5. Use a separate bearer token for each client when practical.
6. Keep arbitrary command execution disabled unless you specifically need and trust it.
7. Adaptive tool loading is a good default for reducing MCP context overhead.

The connector runs its MCP server **inside Obsidian**, on loopback (`127.0.0.1`). Obsidian therefore needs to be running for the connector to work.

### Claude Desktop connection

The recommended Claude Desktop path is the connector's `.mcpb` bundle:

1. In **MCP Connector → Access control**, click **`.mcpb`** on the token row.
2. Drag the generated `.mcpb` file onto Claude Desktop.
3. Confirm it appears under **Claude Desktop → Settings → Extensions**.
4. Restart Claude Desktop if necessary.

Avoid committing Obsidian MCP bearer tokens. They are credentials.

### Test the connection

In Claude Desktop, try:

```text
Read brain/PROJECT.md using the Obsidian connector. Do not modify anything.
```

Then test a small write and Canvas operation.

---

## 5. Create a Claude Project for brainstorming

Create a Claude Project for the repository.

Copy the contents of:

```text
setup/CLAUDE_PROJECT_INSTRUCTIONS.md
```

into the Claude Project's **Project Instructions** field.

**Important:** this connection is manual. Claude Projects do not automatically discover, read, or sync this file from your local repository. The file exists in the repo so the instructions are version-controlled and reusable across projects.

The relationship is:

```text
repo/setup/CLAUDE_PROJECT_INSTRUCTIONS.md
        │
        │ manual copy/paste
        ▼
Claude Project → Project Instructions
```

By contrast, `CLAUDE.md` is repository-level guidance used by Claude Code when it works in the repo. These are separate mechanisms.

Customize only the short **Project Context** section before pasting. Keep detailed and evolving feature knowledge in Obsidian rather than duplicating it in Project Instructions.

The intended loop is:

```text
Claude Project discussion
        ↓
durable conclusions
        ↓
Obsidian MCP
        ↓
PROJECT.md / Features / Decisions / PROJECT.canvas
```

During normal brainstorming, Claude should checkpoint durable knowledge rather than documenting every message.

A useful maintenance command is:

```text
Reconcile the project brain
```

---

## 6. Obsidian conventions

### `PROJECT.md`

Use as the concise index for:

- Major Areas
- Features
- important Decisions
- Open Questions

Prefer links to Feature notes instead of duplicating detailed content.

### `Features/`

Feature notes are living descriptions of the current understanding of a feature, not meeting logs.

### `Decisions/`

Use lightweight ADRs only when the reasoning behind a decision is likely to matter later.

### `PROJECT.canvas`

Use Canvas for:

- Major Areas
- Features
- meaningful dependencies
- cross-area relationships
- important decisions when useful

For a brand-new Canvas, plan the initial layout before writing it. After a meaningful layout exists, prefer localized edits and preserve manual rearrangements.

---

## 7. Install GitHub Spec Kit

Spec Kit is optional but useful once brainstorming turns into implementation work.

Install the Specify CLI following the current Spec Kit documentation. A typical installation is:

```bash
uv tool install specify-cli
```

Then initialize Spec Kit for the project using the integration appropriate for your coding agent.

After initialization, the core workflow is:

```text
constitution
→ specify
→ clarify (when useful)
→ plan
→ checklist (when useful)
→ tasks
→ analyze
→ implementation
→ review
```

The standard Spec Kit commands include:

```text
/speckit.constitution
/speckit.specify
/speckit.clarify
/speckit.plan
/speckit.checklist
/speckit.tasks
/speckit.analyze
/speckit.implement
```

This template intentionally treats **Obsidian as evolving project memory** and **Spec Kit as the approved implementation contract**.

A useful handoff phrase in the Claude Project is:

```text
Prepare this feature for specification
```

That should produce the stable intent, agreed behavior, constraints, edge cases, dependencies, non-goals, blockers, and relevant decisions needed to begin Spec Kit work.

---

## 8. Claude Code

Open Claude Code from the project root.

Keep durable coding-agent guidance in:

```text
CLAUDE.md
AGENTS.md
```

A useful split is:

- `AGENTS.md` — concise implementation rules shared across coding agents.
- `CLAUDE.md` — Claude-specific planner/reviewer behavior and delegation rules.

Example principle:

```text
A strong lead model owns requirements refinement, architecture planning,
acceptance criteria, and independent review. Routine implementation may be
delegated to a lower-cost implementation model.
```

Do not duplicate detailed feature requirements here; those belong in Spec Kit.

---

## 9. Optional: connect Claude Code to Codex through MCP

This is useful if you want Claude Code to act as planner/reviewer while Codex acts as an implementation worker.

Codex exposes an experimental stdio MCP server:

```bash
codex mcp-server
```

To make it available to Claude Code across your projects, add it at **user scope**:

```bash
claude mcp add --transport stdio --scope user codex -- codex mcp-server
```

Verify:

```bash
claude mcp list
```

User-scoped MCP servers are machine/user configuration; they should not be committed to this template.

A simple division of labor is:

```text
Claude / strong lead model
  → refine requirements
  → architecture / planning
  → acceptance criteria
  → independent code review

Codex / implementation model
  → implement bounded tasks
  → run tests
  → report DONE / BLOCKED / SPEC-CONFLICT
```

The reviewer should review the actual diff and tests independently rather than merely accepting the implementer's reasoning.

Codex's MCP server interface is experimental, so check current Codex documentation if the command or interface changes.

---

## 10. Suggested feature workflow

```text
1. Brainstorm in Claude Project.
2. Claude checkpoints durable conclusions into Obsidian.
3. You inspect/rearrange PROJECT.canvas when useful.
4. When a feature is mature, say: "Prepare this feature for specification."
5. Move to Claude Code.
6. Run Spec Kit specification/planning/tasks.
7. Resolve ambiguities before implementation.
8. Delegate bounded implementation if desired.
9. Run tests.
10. Have a strong model independently review the diff against the spec.
11. Open a GitHub PR / run CI.
12. Merge.
```

Requirements are not permanently frozen. During an implementation cycle, the approved revision should be treated as read-only. If implementation exposes a requirement conflict, revise and approve the spec rather than silently changing scope.

---

## 11. Git and security

Before publishing or turning a repository into a public template:

Never commit:

```text
.env
API keys
bearer tokens
MCP tokens
exchange credentials
private certificates
machine-specific secrets
```

Recommended Obsidian ignores:

```gitignore
brain/.obsidian/workspace.json
brain/.obsidian/workspace-mobile.json
```

Review plugin configuration before committing `.obsidian/`. Some plugins store secrets or machine-specific state in plugin `data.json` files.

A public template should contain configuration **examples**, never real credentials.

---

## 12. Context-efficiency tips

MCP-heavy workflows can consume conversation context quickly.

Useful practices:

- use adaptive MCP tool loading where available;
- read known files directly rather than repeatedly listing the whole vault;
- prefer partial or batched reads when full file contents are unnecessary;
- patch existing notes instead of rewriting them wholesale;
- plan Canvas changes before calling tools;
- batch Canvas operations when supported;
- avoid repeated verification reads;
- start a fresh chat after large one-time initialization/import operations.

The goal is incremental maintenance, not repeated reconstruction of the project brain.

---

## 13. What belongs where?

```text
Claude Project Instructions
→ stable project identity and reasoning behavior
→ rules for maintaining Obsidian

Obsidian
→ evolving product/system understanding
→ Features
→ Decisions
→ Open Questions
→ visual Canvas

Spec Kit
→ approved feature requirements
→ implementation plan
→ tasks
→ consistency checks

Git/GitHub
→ source code
→ history
→ PRs
→ CI
```

---

## 14. New-project checklist

For each new project:

```text
Use GitHub template
→ clone locally
→ open brain/ in Obsidian
→ enable/confirm MCP Connector
→ create Claude Project
→ paste setup/CLAUDE_PROJECT_INSTRUCTIONS.md into Claude Project Instructions
→ customize Project Context
→ begin brainstorming
→ initialize Spec Kit when implementation is ready
```

Machine-level MCP connections such as Claude Code → Codex should normally be configured once per machine, not once per repository.

---

## Notes

This is a workflow template, not a required stack. You can use only the layers that are useful to you.

The core idea is simple:

**conversation should remain lightweight; durable knowledge should live in files; approved implementation intent should become a spec; code should remain reviewable and versioned.**
