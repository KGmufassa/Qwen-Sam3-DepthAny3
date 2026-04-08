Best practical approach

The most effective pattern is:

- **all slices: prioritize at a high level**
  - core
  - release-critical
  - optional
- **current slice only: prioritize deeply**
  - must do first
  - parallelizable
  - blocked tasks
  - exact execution order

That gives you:
- roadmap clarity across the whole MVP
- execution clarity where you actually need it now

## My recommendation

Do this in two layers:

### Layer 1: Whole-program priority map
Across all slices:
- `Core build`
- `MVP feature-complete`
- `Release hardening`
- `Optional enhancement`

### Layer 2: Deep priority only for Slice 1
Because Slice 1 is what you can actually start implementing now.

That is the most efficient path and avoids overplanning.

If you want, I can do exactly that next:
1. create a **cross-slice priority map**
2. then create a **deep prioritized execution order for Slice 1
