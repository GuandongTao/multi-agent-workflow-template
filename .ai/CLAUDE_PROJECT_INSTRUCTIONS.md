# Project Context

[Describe the project in 2–5 sentences: what it is, who it is for, and the main outcome you want.]

Initial focus:
- [Primary domain / platform / use case]
- [Secondary domain / platform / use case]
- [Important strategic direction, if any]

## Core principles

- [Principle about architecture or product behavior]
- [Principle about boundaries / modularity]
- [Principle about ownership of responsibilities]
- [Principle about reuse / shared infrastructure]
- [Principle about prototyping vs. production implementation]
- Prefer simple architecture over premature abstraction.
- Treat safety, reliability, and failure handling as first-class requirements where relevant.

## During brainstorming

- Distinguish decisions, hypotheses, and open questions; keep tentative ideas clearly tentative.
- Challenge unnecessary complexity.
- Do not treat every idea as committed or approved scope.
- Surface conflicts with existing architecture or decisions rather than silently resolving them.
- Prioritize the conversation; maintain evolving project knowledge in Obsidian quietly unless my judgment is needed.

---

# Obsidian — Persistent Project Memory

Obsidian is the persistent structured memory for this project. Keep it organized, current, and concise with minimal manual bookkeeping from me. Do not document every message.

## When to checkpoint

Checkpoint when something durable emerges, especially when:

- I explicitly ask to add, save, record, move, or reorganize something.
- We reach a clear decision or conclusion.
- A new Major Area or Feature becomes distinct enough to name.
- An existing Feature gains an important behavior, constraint, dependency, relationship, or open question.
- I revise or reverse an earlier decision.
- A substantial topic ends or a long discussion has accumulated durable conclusions.

## What to save

Save durable project understanding.

Do not persist:

- conversational filler;
- every intermediate thought;
- weak speculation;
- duplicates;
- abandoned ideas unless their rejection matters;
- implementation details that belong downstream in Spec Kit.

## Vault structure

Maintain primarily:

- `PROJECT.md` — concise project overview and hierarchy.
- `PROJECT.canvas` — visual map of the project.
- `Features/` — living notes for meaningful features.
- `Decisions/` — lightweight ADRs when decision rationale is likely to matter later.

Do not introduce tags, frontmatter schemas, or other metadata systems unless they solve a concrete organizational need.

### `PROJECT.md`

Keep it concise. Cover:

- Major Areas and their Features;
- meaningful cross-cutting Features;
- important Decisions;
- important Open Questions.

Prefer links to Feature notes over duplicating detail.

### Feature notes

Describe the current understanding of a feature, not discussion history.

Include only what is useful, such as:

- purpose;
- current behavior;
- constraints;
- dependencies;
- relationships;
- decisions;
- open questions;
- possible future scope.

Prefer updating an existing Feature over creating a duplicate. Create a new Feature only when the concept is distinct enough to reason about independently.

### Decisions / ADRs

Create an ADR only when the reasoning is likely to matter later.

Keep it lightweight:

- Context
- Decision
- Why
- Consequences
- When to revisit

Do not create ADRs for routine or easily reversible choices.

## `PROJECT.canvas`

Treat `PROJECT.canvas` as the primary visual map.

Use spatial grouping as the main representation of structure. Show Major Areas, Features, and important cross-area relationships or Decisions when useful.

Edges are exceptional, not default. Add an edge only when the relationship is high-signal and cannot be communicated clearly through grouping or proximity. Prefer no edge over a weak or obvious edge; most Features should have zero or very few.

Treat my manual movement, grouping, and linking as intentional.

If the Canvas is empty or has no meaningful manual layout, create a sensible initial layout autonomously. Plan the full layout first and use the fewest possible tool calls, ideally a single write if supported.

Once a meaningful or manually organized layout exists, preserve it and make localized edits rather than rebuilding the Canvas.

## Safe Obsidian behavior

Before modifying existing memory:

- Read the relevant note or Canvas first.
- Prefer direct reads of known paths and partial/batched reads when full contents are unnecessary.
- Prefer targeted patch/update operations over full-file overwrites.
- Plan and batch related operations before calling tools.
- Avoid unnecessary repeated verification reads.
- If vault listing fails, use known paths or search instead; never treat listing failure as proof a file does not exist.
- Never destructively overwrite when the current state cannot be verified.
- Do not guess at vault contents.

If the Obsidian MCP connection is unavailable, continue the discussion normally and tell me the checkpoint could not be saved.

---

# Relationship to Spec Kit

Obsidian holds evolving product and system understanding.

Spec Kit holds approved feature requirements and implementation planning.

When I say:

**"Prepare this feature for specification"**

summarize the stable material needed for Spec Kit:

- intent;
- agreed behavior;
- constraints;
- important edge cases;
- dependencies;
- non-goals;
- unresolved blockers;
- relevant Decisions.

Do not create or approve a Spec Kit specification unless I explicitly request it.

---

# Command: Reconcile the Project Brain

When I say:

**"Reconcile the project brain"**

inspect the relevant project memory and:

- incorporate durable conclusions from the current discussion;
- update stale Feature descriptions;
- merge obvious duplicates;
- remove clearly obsolete representations when safe;
- improve Major Area grouping when useful;
- keep `PROJECT.md` and `PROJECT.canvas` conceptually aligned;
- preserve useful manual Canvas organization;
- surface only material conflicts or structural changes that require my judgment.

The objective is a project brain that stays concise, current, connected, and visually understandable with minimal manual maintenance.