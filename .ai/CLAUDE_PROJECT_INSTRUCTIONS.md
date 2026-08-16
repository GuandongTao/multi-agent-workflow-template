\# Project Context



\[Describe this project in 2–5 sentences.]



Core principles:

\- \[...]

\- \[...]

\- \[...]



During brainstorming:

\- distinguish decisions, hypotheses, and open questions;

\- challenge unnecessary complexity;

\- do not treat every idea as committed scope;

\- keep evolving project knowledge in Obsidian.



\# Obsidian Project Memory



\# Obsidian — Persistent Project Memory



Obsidian is the persistent structured memory for this project: organized project knowledge with minimal manual bookkeeping from me. Do not document every message.



\## When to checkpoint



Checkpoint when something durable emerges, especially when:



\- I explicitly say to add, save, record, move, or reorganize something.

\- We reach a clear decision or conclusion.

\- A new Major Area or Feature becomes distinct enough to name.

\- An existing Feature gains an important behavior, constraint, dependency, relationship, or open question.

\- I revise or reverse an earlier decision.

\- We finish a substantial topic or a long discussion has accumulated useful conclusions.



\## What to save (and not)



Save durable project understanding. Do \*\*not\*\* persist conversational filler, every intermediate thought, weak speculation, duplicates, abandoned ideas (unless their rejection matters), or implementation details that belong downstream in Spec Kit.



\## Vault structure



Maintain primarily:



\- `PROJECT.md` — concise project overview and hierarchy.

\- `PROJECT.canvas` — visual map of the project.

\- `Features/` — living notes for meaningful features.

\- `Decisions/` — lightweight ADRs when rationale is likely to matter later.



Don't introduce tags, frontmatter schemas, or other metadata systems unless they solve a concrete organizational need.



\*\*`PROJECT.md`\*\* — keep concise. Cover Major Areas and their Features, meaningful cross-cutting Features, important Decisions, and important Open Questions. Prefer links to Feature notes over duplicating detail.



\*\*Feature notes\*\* — describe current understanding, not discussion history. Include only what's useful: purpose, current behavior, constraints, dependencies, relationships, decisions, open questions, possible future scope. Update an existing Feature rather than duplicating; create a new one only when the concept is distinct enough to reason about independently.



\*\*Decisions (ADRs)\*\* — create only when the reasoning is likely to matter later, not for routine or easily reversible choices. Keep lightweight: Context, Decision, Why, Consequences, When to revisit.



\## PROJECT.canvas



The primary visual map. Show Major Areas, Features, meaningful dependencies, cross-area relationships, and important Decisions when useful. Prefer useful spatial grouping over exhaustive linking; don't add edges for weak or obvious relationships.



Treat my manual movement, grouping, and linking as intentional. If the Canvas is empty or has no meaningful manual layout, create a sensible initial layout autonomously — plan it fully first and write it in the fewest possible tool calls (a single write if supported). Once I've reorganized it, preserve my layout and make localized edits rather than rebuilding.



\## Safe Obsidian behavior



Before modifying existing memory:



\- Read the relevant note or Canvas first; prefer direct reads of known paths, and partial/batched reads when full contents aren't needed.

\- Prefer targeted patch/update operations over full-file overwrites.

\- Plan and batch related operations before calling tools; avoid repeated verification reads.

\- Use search or known paths as fallback if listing fails; never treat a listing failure as proof a file doesn't exist.

\- Never destructively overwrite if the current state can't be verified. Don't guess at vault contents.



If the Obsidian MCP connection is unavailable, continue normally and tell me the checkpoint couldn't be saved.



\---



\# Relationship to Spec Kit



Obsidian holds evolving product and system understanding. Spec Kit holds approved feature requirements and implementation planning.



\*\*"Prepare this feature for specification"\*\* → summarize the stable material for Spec Kit: intent, agreed behavior, constraints, important edge cases, dependencies, non-goals, unresolved blockers, relevant Decisions. Do not create or approve a Spec Kit specification unless I explicitly request it.



\# Command: Reconcile the project brain



When I say \*\*"Reconcile the project brain"\*\*, inspect the relevant memory and:



\- Incorporate durable conclusions from the current discussion.

\- Update stale Feature descriptions; merge obvious duplicates; remove clearly obsolete representations when safe.

\- Improve Major Area grouping if useful.

\- Keep `PROJECT.md` and `PROJECT.canvas` conceptually aligned; preserve useful manual Canvas organization.

\- Surface only material conflicts or structural changes that require my judgment.



Objective: a project brain that stays concise, current, connected, and visually understandable without manual maintenance from me.

