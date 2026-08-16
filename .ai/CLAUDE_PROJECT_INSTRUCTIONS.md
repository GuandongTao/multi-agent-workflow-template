# Project Context

[Describe the project in 2–5 sentences: what it is, who/what it serves, and the main outcome.]

Initial focus:
- [Primary area / platform / use case]
- [Secondary area, if relevant]
- [Important strategic direction, if relevant]

## Principles

- [Important architecture/product principle]
- [Important boundary or modularity principle]
- [Important responsibility/ownership principle]
- [Important reuse or consistency principle]
- Prefer simple architecture over premature abstraction.
- Treat safety, reliability, and failure handling as first-class where relevant.

During brainstorming, distinguish decisions, hypotheses, and open questions; keep tentative ideas tentative; challenge unnecessary complexity; do not treat brainstorming as approved scope; surface conflicts rather than silently resolving them.

---

# Obsidian Project Memory

Obsidian is the durable project memory.

Do not access it during normal brainstorming unless I explicitly request it. Use conversation/project memory when sufficient.

- **"Save this"** → persist the directly relevant conclusion.
- **"Sync brain"** → persist durable conclusions since the last successful sync.
- **"Reconcile project brain"** → rare broader cleanup/alignment pass.

## Structure

Maintain primarily:

- `PROJECT.md` — concise index of Major Areas, Features, important Decisions, and project-level Open Questions.
- `Features/` — current understanding of meaningful features.
- `Decisions/` — lightweight ADRs when rationale matters.
- `PROJECT.canvas` — high-level visual map.

Do not add tags, frontmatter schemas, or other metadata systems without a concrete need.

Save durable understanding, not conversational history, weak speculation, duplicates, superseded detail, or implementation material that belongs in Spec Kit.

### Feature notes

Keep Feature notes concise and current-state oriented. Replace stale text when conclusions change rather than appending chronological history. Preserve old reasoning only when still useful; move consequential rationale into an ADR.

Create a new Feature only when it is distinct enough to reason about independently.

### Decisions

Create ADRs only for consequential decisions whose reasoning may matter later. Keep them lightweight: Context, Decision, Why, Consequences, When to revisit.

### `PROJECT.md`

Touch `PROJECT.md` only when hierarchy, cross-cutting structure, important Decisions, or project-level Open Questions are affected. Local Feature changes should remain local.

### `PROJECT.canvas`

Canvas is a visual overview, not a live dependency graph.

Update it only when explicitly requested or when a Major Area/Feature is created, moved, merged, or removed.

Use spatial grouping as the primary structure. Edges are exceptional; add only high-signal relationships that proximity/grouping cannot express.

Preserve manual layout. If Canvas is empty, create a sensible initial layout efficiently; afterward prefer localized edits.

## Efficient & safe Obsidian use

Before calling tools, identify the likely affected files and start with the smallest reasonable set. Expand when hierarchy, cross-feature relationships, Decisions, or Open Questions may also be affected.

- Use known paths directly; avoid vault-wide discovery unless needed.
- Prefer partial/direct reads when sufficient; read full notes when surrounding context is needed for correctness.
- Prefer targeted patches over full-file overwrites.
- Assume successful writes succeeded; do not reread solely for verification.
- If unsure about blast radius, spend the extra read rather than risk missing an update.
- Never overwrite unverified content or guess at vault state.

If MCP is unavailable, continue the discussion and report that the requested save/sync was not completed.

---

# Spec Kit

Obsidian holds evolving understanding; Spec Kit holds approved requirements and implementation planning.

**"Prepare this feature for specification"** → summarize stable:
- intent
- agreed behavior
- constraints
- important edge cases
- dependencies
- non-goals
- unresolved blockers
- relevant Decisions

Do not create or approve a Spec Kit specification unless explicitly requested.

## Reconcile

When I say **"Reconcile project brain"**, update stale material, merge duplicates, safely remove obsolete representations, improve hierarchy where useful, align `PROJECT.md` and Canvas, preserve manual layout, and surface only conflicts or structural changes requiring my judgment.