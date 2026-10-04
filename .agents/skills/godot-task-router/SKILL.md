---
name: godot-task-router
description: Classifies Godot project tasks before work, scores scope and architectural risk, and routes design/planning/research to Antigravity and implementation/testing to Codex. Use before any Godot project task, especially when deciding whether to accept, defer, split, or review work.
---

# Godot Task Router

## Mandatory first step

Before changing any project file, classify the requested task. You may inspect relevant project files read-only to resolve uncertainty. Do not start implementation before stating the routing decision.

Read the relevant references in this skill: `references/complexity.md`, `references/codex-role.md`, `references/antigravity-role.md`, and `references/handoff.md`.

## Classification procedure

1. Identify the requested outcome and the current agent (Codex or Antigravity). If the current agent is unknown, state that the routing decision assumes the current application/model role.
2. Inspect only the relevant project context read-only when needed: `project.godot`, nearby scripts/scenes/resources, and existing architecture/instructions. Do not invent file counts or affected systems; mark estimates as estimates.
3. Identify task kind: implementation, architecture/planning, research, review, simple fix, complex cross-system bug, or major feature.
4. Score complexity using `references/complexity.md`. Apply escalation overrides regardless of score. Complexity alone never decides ownership.
5. Check the current agent against the role matrix.
6. Output the routing decision first. If DEFER, stop: no project edits, code, or partial implementation. Provide a useful handoff.
7. If ACCEPT, state scope, risks, acceptance criteria, and verification approach, then do only the owned work. Reclassify if inspection reveals a material scope or architecture change.

## Ownership summary

- **Antigravity:** architecture, feature/system design, requirements clarification, research, decomposition of major work, and review of completed major features.
- **Codex:** code and scene/resource implementation from a clear request or approved spec, bug fixes, refactors that preserve architecture, tests, Godot CLI validation, and implementation-level optimization.
- **Complex cross-system bug:** Antigravity diagnoses and writes a focused debugging plan; Codex implements the fix and validates it.
- **Major feature:** Antigravity produces an implementation spec and task breakdown; Codex implements and tests; Antigravity reviews against the spec.

This is a human-mediated handoff. Do not claim to have called or assigned work to the other app unless an actual integration is available and used.

## Required first response format

```text
ROUTING DECISION: ACCEPT | DEFER TO CODEX | DEFER TO ANTIGRAVITY | NEEDS CLARIFICATION
TASK TYPE: ...
COMPLEXITY SCORE: ... / CLASS: ...
WHY: ...
NEXT STEP: ...
```

When deferring, use the handoff format in `references/handoff.md` and stop. When accepting, keep the initial classification concise and proceed.

## Hard stop rules

- If architecture/persistence/networking/core-system override applies, Codex must defer before implementation.
- If task ownership belongs to another agent, never implement “just a small part” unless the user explicitly narrows the request into an owned task.
- If requirements are materially ambiguous, ask a short clarification or defer to Antigravity; do not pick a major architecture by guess.
- Do not modify unrelated systems or files. Do not create a new autoload/global manager, dependency, or save format without an approved design.
- A DEFER result must not alter project files. Read-only inspection and a handoff document in the conversation are allowed.
