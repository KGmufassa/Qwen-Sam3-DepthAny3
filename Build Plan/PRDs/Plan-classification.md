# Plan Classification

This classification separates the optimized MVP plans into four buckets:

- `Independent plans`
- `Draft-first plans`
- `Dependency-sensitive plans`
- `Finalization order`

---

## 1. Independent Plans

These can be written in substantial detail immediately, without waiting on implementation or model integration.

### Fully independent

- `MVP Scope Plan`
- `Decision Log Plan`
- `Dependency Gate Plan`
- `Unified Architecture Plan`
- `Mock-First Integration Plan`
- `Fallback UX Plan`
- `Deployment And Infrastructure Plan`
- `QA And Release Readiness Plan`
- `Vertical Release Slice Plan`

### Why these are independent

They define:
- scope
- sequencing
- responsibilities
- operating assumptions
- failure posture
- delivery strategy

They do not require working code, live workers, or finalized schema details to begin.

---

## 2. Draft-First Plans

These should be written early, but treated as strong drafts until a few core decisions are frozen.

### Draft-first

- `Editor UX And Interaction Plan`
- `State And History Plan`
- `Caching And Performance Plan`
- `Artifact And Export Lifecycle Plan`

### Why these are draft-first

They depend on likely-stable concepts, but not fully-final contracts yet.

Examples:
- editor UX depends on what a `Layer` really is
- history rules depend on whether async jobs create versions or replace assets
- caching depends on checksum boundaries and artifact identity rules
- export lifecycle depends on how preview and export consume the scene graph

These plans should start early so product and engineering can align, but they will likely need one revision pass.

---

## 3. Dependency-Sensitive Plans

These plans should not be finalized until the core system contracts are frozen.

### High dependency sensitivity

- `Data Schema And Scene Graph Plan`
- `API And Job Contract Plan`
- `Canonical Math Plan`
- `Worker Runtime Contract Plan`

### Why these are dependency-sensitive

These are foundational contract documents. Other plans and implementation work will depend on them directly.

They require decisions such as:
- what entities exist in the system
- what the authoritative scene graph looks like
- what coordinate spaces are canonical
- what workers own vs what the app owns
- what request/response contracts look like
- how artifacts are registered and referenced

If these are finalized too early without enough decision clarity, they will cause rework everywhere else.

---

## 4. Hidden Dependency Notes

Some plans look independent but still rely on a small number of upstream decisions.

### Low hidden dependency
- `Unified Architecture Plan`
- `Deployment And Infrastructure Plan`

These need:
- the basic control-plane/worker-plane split
- whether workers are local, remote, or hybrid
- whether the app is source of truth

### Medium hidden dependency
- `Editor UX And Interaction Plan`
- `Artifact And Export Lifecycle Plan`

These need:
- final layer semantics
- final artifact registration model
- preview/export relationship

### High hidden dependency
- `Canonical Math Plan`
- `Data Schema And Scene Graph Plan`
- `API And Job Contract Plan`

These should be treated as freeze points.

---

# Finalization Order

This is the recommended order for turning draft plans into frozen plans.

## Stage 1: Freeze strategy first

Finalize:

1. `MVP Scope Plan`
2. `Decision Log Plan`
3. `Dependency Gate Plan`
4. `Unified Architecture Plan`

### Outcome
You now know:
- what MVP is
- what is excluded
- which major decisions are already made
- the high-level shape of the system

---

## Stage 2: Freeze core contracts

Finalize:

5. `Data Schema And Scene Graph Plan`
6. `Canonical Math Plan`
7. `API And Job Contract Plan`
8. `Worker Runtime Contract Plan`

### Outcome
You now know:
- what the system stores
- how layers and artifacts are modeled
- how requests move through the system
- what each worker must accept and return

This is the most important freeze point in the whole planning process.

---

## Stage 3: Finalize workflow behavior

Finalize:

9. `Editor UX And Interaction Plan`
10. `State And History Plan`
11. `Fallback UX Plan`
12. `Artifact And Export Lifecycle Plan`

### Outcome
You now know:
- how users move through the product
- how editing behaves
- how failures are surfaced
- how outputs are persisted and exported

---

## Stage 4: Finalize platform and delivery

Finalize:

13. `Deployment And Infrastructure Plan`
14. `Caching And Performance Plan`
15. `QA And Release Readiness Plan`
16. `Vertical Release Slice Plan`

### Outcome
You now know:
- how the system runs
- how it scales
- how it is tested
- how it is delivered incrementally

---

# Classification Table

| Plan | Classification | Finalize When |
|---|---|---|
| MVP Scope Plan | Independent | Stage 1 |
| Decision Log Plan | Independent | Stage 1 |
| Dependency Gate Plan | Independent | Stage 1 |
| Unified Architecture Plan | Independent | Stage 1 |
| Data Schema And Scene Graph Plan | Dependency-sensitive | Stage 2 |
| Canonical Math Plan | Dependency-sensitive | Stage 2 |
| API And Job Contract Plan | Dependency-sensitive | Stage 2 |
| Worker Runtime Contract Plan | Dependency-sensitive | Stage 2 |
| Editor UX And Interaction Plan | Draft-first | Stage 3 |
| State And History Plan | Draft-first | Stage 3 |
| Fallback UX Plan | Independent | Stage 3 |
| Artifact And Export Lifecycle Plan | Draft-first | Stage 3 |
| Deployment And Infrastructure Plan | Independent | Stage 4 |
| Caching And Performance Plan | Draft-first | Stage 4 |
| QA And Release Readiness Plan | Independent | Stage 4 |
| Vertical Release Slice Plan | Independent | Stage 4 |

---

# Practical Recommendation

Use this working rule:

- `Independent plans` can be written and approved now
- `Draft-first plans` should be written now, then revised once contracts freeze
- `Dependency-sensitive plans` should be outlined now but only finalized after Stage 1 decisions are locked

That gives you the fastest planning velocity with the least rework.

## Best immediate next move

Start by fully writing these four first:

1. `MVP Scope Plan`
2. `Decision Log Plan`
3. `Unified Architecture Plan`
4. `Dependency Gate Plan`

Those four unlock the rest of the planning stack cleanly.
