# Fallback UX Plan

## Document Purpose

This document defines how the product should behave when the ideal path fails, degrades, or becomes ambiguous.

It focuses on:

- segmentation failures
- stitching issues
- depth issues
- worker unavailability
- export problems
- responsiveness/parallax mismatches

Fallback behavior is part of MVP quality, not optional polish.

---

## Fallback Principles

- failure must be visible
- failure must be actionable
- users should not lose scene state because one stage failed
- fallback behavior should preserve trust
- system-generated uncertainty should not be hidden

---

## Failure Categories

The MVP should plan for at least these failure classes:

- upload failure
- stitch failure
- segmentation failure
- extraction failure
- depth failure
- group/parallax configuration confusion
- worker unavailable
- job timeout
- export failure

---

## Upload Fallback

If upload fails:

- the user should know which image failed
- the user should be able to retry that upload
- already uploaded images should not be discarded automatically

---

## Stitch Fallback

If stitching fails or produces weak output:

- the user should see that the stitched scene is not ready
- the system should identify the failed stage explicitly
- the user should be able to retry the stitch job
- source image registrations should remain intact

If future manual stitch tuning is added, it should be separate from the MVP baseline.

---

## Segmentation Fallback

If segmentation quality is poor:

- the user should see that the issue is segmentation quality, not a broken editor
- the user should be able to retry or submit revised prompts
- unaccepted segmentation candidates should not silently become layers

The fallback should not be “start over from scratch” unless truly necessary.

---

## Extraction Fallback

If layer extraction fails:

- the corresponding layer should not appear as if it is ready
- failed extraction should be visible at the layer/job level
- the user should be able to retry extraction

Partial success should be preserved for unaffected layers.

---

## Depth Fallback

If depth generation fails:

- the scene should still be editable
- the user should be informed that default parallax suggestions are unavailable
- retry should be available

If depth output is semantically wrong:

- the user must be able to manually override parallax behavior
- the product should not treat depth as unquestionable truth

---

## Group And Parallax Fallback

If grouped behavior looks wrong:

- the user should be able to inspect inherited versus overridden values
- the user should be able to remove a layer from a group
- the user should be able to adjust group mapping without rewriting the scene

If medium-specific behavior feels wrong:

- the user should be able to preview per medium
- the user should be able to adjust group-level medium overrides

---

## Worker Unavailability Fallback

If one worker family is unavailable:

- the UI should identify which capability is unavailable
- unaffected editing features should remain usable
- the user should not be blocked from inspecting or editing already-saved state

Examples:

- if depth worker is unavailable, layer editing still works
- if refine worker is unavailable, baseline scene editing still works

---

## Timeout Fallback

If a job times out:

- the job should move to a visible failed or timeout state
- the user should have a retry path
- the UI must not remain in indefinite loading

---

## Export Fallback

If export fails:

- the scene state must remain intact
- the error must be visible
- retry must be available
- export failure must not imply scene corruption

If export succeeds but preview/export fidelity mismatch is detected:

- this should be surfaced as a quality issue, not silently ignored

---

## Partial Completion UX

The MVP must tolerate partial completion.

Examples:

- some layers extracted, others failed
- stitched scene ready, depth pending
- preview available, export pending

The UI should communicate what is:

- ready
- pending
- failed
- retryable

---

## State Preservation Rules

Fallback UX should preserve:

- saved groups
- saved layer order
- saved transforms
- saved parallax settings
- saved responsive overrides

A failed worker stage must not wipe working scene configuration.

---

## Error Messaging Rules

Error messaging should aim for:

- stage clarity
- user action clarity
- no backend jargon unless needed for diagnosis

Good examples:

- `Depth generation failed. You can keep editing and retry depth later.`
- `This layer extraction failed. Retry extraction for this layer.`

---

## Out-Of-Scope Fallback Features

The MVP does not require:

- advanced guided repair assistants
- automatic intelligent fallback generation for every failure
- collaborative error-resolution tooling

---

## Freeze Criteria

This plan is ready to freeze when:

- failure categories are accepted
- fallback preservation rules are accepted
- retry expectations are accepted
- worker unavailability behavior is accepted

---

## Final Fallback Statement

The MVP fallback UX treats failures as visible, recoverable state transitions rather than hidden breakdowns, preserving as much stitched scene configuration as possible while giving users clear retry paths and keeping unaffected editing features usable.
