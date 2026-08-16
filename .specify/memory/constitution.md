<!--
Sync Impact Report
==================
Version change: (unratified template) → 1.0.0
Bump rationale: Initial ratification. First concrete constitution replacing the
  unfilled scaffold; MAJOR baseline established.

Principles defined (Core Principles):
  - I. Correctness & Determinism (new)
  - II. Observability & Auditability (new)
  - III. Risk Controls & Safety (new)

Sections added:
  - Agent Roles & Development Workflow (from user-authored governance content)
  - Architecture & The Ponytail Rule (from user-authored governance content)
  - Testing & Review Standards (from user-authored governance content)
  - Governance (amendment, versioning, and compliance policy)

Sections removed: none (initial ratification)

Placeholders resolved: PROJECT_NAME, all PRINCIPLE_*, SECTION_2/3_*, GOVERNANCE_RULES,
  CONSTITUTION_VERSION, RATIFICATION_DATE, LAST_AMENDED_DATE.

Deferred TODOs: none.
-->

# trade_infra Constitution

## Core Principles

### I. Correctness & Determinism

- **Deterministic critical paths**: Order lifecycle, position accounting, and market-data
  processing MUST produce identical outputs for identical inputs and MUST NOT depend on
  wall-clock timing, iteration order, or uninitialized state.
- **No undefined states**: Every state transition in trading logic MUST be explicit. Unknown
  or unreachable states MUST fail closed (reject/halt) rather than proceed on a guess.
- **Exact numeric handling**: Money, quantities, and prices MUST use exact/decimal
  representations; floating-point MUST NOT be used where rounding can alter fills, balances,
  or P&L.
- **Rationale**: In trading infrastructure, a non-deterministic or silently incorrect result is
  indistinguishable from a loss event and cannot be reconstructed after the fact.

### II. Observability & Auditability

- **Structured logging**: All trading actions (order submit/amend/cancel, fills, risk
  decisions) MUST emit structured, machine-parseable log records with correlation identifiers.
- **Immutable audit trail**: Every action that affects orders, positions, or capital MUST be
  recorded in an append-only audit trail sufficient to reconstruct the decision after the fact.
- **Metrics on critical paths**: Latency, error, and rejection metrics MUST be exposed for the
  order and market-data paths; silent failure is a defect.
- **Rationale**: If an action cannot be observed and later reconstructed, it cannot be debugged,
  reviewed, or defended.

### III. Risk Controls & Safety

- **Fail-safe defaults**: Anything touching live orders or capital MUST default to the safe
  state (no order, no exposure) when configuration, connectivity, or validation is uncertain.
- **Hard limits & kill-switches**: Enforceable position, order-rate, and exposure limits plus a
  reachable kill-switch MUST exist before any code path can place live orders.
- **Explicit live-vs-simulated boundary**: Live-trading paths MUST be unambiguously distinct
  from simulated/backtest paths and MUST require explicit, auditable enablement.
- **Rationale**: Safety controls that are optional or added later are, in practice, absent when
  they are most needed.

## Agent Roles & Development Workflow

- **Lead Model (Planner/Reviewer)**: A strong Claude or GPT-class model is responsible for
  specification refinement, architectural planning, acceptance criteria, and independent code
  review.
- **Implementation Model**: Routine implementation should be delegated to the designated
  cost-effective coding model, working from the approved specification and plan.
- **Direct Implementation Exception**: The lead model may implement trivial or tightly bounded
  changes when explicitly requested or when delegation would add unnecessary overhead.
- **No Silent Requirement Drift**: Approved product requirements are read-only during an
  implementation cycle. If implementation reveals ambiguity, conflict, or necessary scope
  change, stop and request a specification revision before continuing.

## Architecture & The Ponytail Rule

- **Simplicity First**: Prefer the simplest architecture that satisfies the current
  requirements. Avoid premature abstraction, unnecessary indirection, heavy generic service
  layers, or speculative extensibility.
- **Built-in First**: Prefer native framework capabilities, standard-library utilities, and
  existing project dependencies before adding new packages.
- **Reuse Without Forced Abstraction**: Reuse or extend existing code when it genuinely reduces
  duplication and complexity. Do not create abstractions solely to achieve reuse.
- **Locality Over Cleverness**: Prefer code whose behavior is easy to understand from nearby
  files over highly generalized or distributed designs.

## Testing & Review Standards

- **Behavioral Testing**: Prioritize tests for externally observable behavior, critical logic,
  regressions, data integrity, and important edge cases rather than arbitrary coverage
  percentages.
- **Implementation-Level Tests**: The implementer may add unit or integration tests appropriate
  to the chosen implementation, but must not weaken approved acceptance criteria merely to make
  the implementation pass.
- **Independent Review**: The final implementation MUST be reviewed by a strong model that did
  not author the implementation, using the approved specification and current diff as primary
  inputs.
- **Small Diffs**: Prefer modular, bounded changes that are easy to inspect and review. Avoid
  unrelated refactoring inside feature work.

## Governance

- **Authority**: This constitution supersedes other development practices. Where a proposed
  approach conflicts with a principle here, the principle wins unless the constitution is first
  amended.
- **Amendment procedure**: Amendments MUST be proposed as an explicit change to this file,
  include the rationale and a version bump, and be reviewed and approved before adoption.
- **Versioning policy** (semantic versioning of governance):
  - **MAJOR**: Backward-incompatible governance changes — removing or redefining a principle.
  - **MINOR**: A new principle/section is added or existing guidance is materially expanded.
  - **PATCH**: Clarifications, wording, or typo fixes with no change in meaning.
- **Compliance review**: Every specification, plan, and code review MUST verify compliance with
  these principles. Deviations MUST be justified in writing and approved, or the work is
  rejected. Unjustified complexity is a compliance failure under the Ponytail Rule.

**Version**: 1.0.0 | **Ratified**: 2026-08-16 | **Last Amended**: 2026-08-16
