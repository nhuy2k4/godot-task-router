# Handoff protocol

A handoff is a message for the user to carry to the other application. It does not automatically transfer a task or grant the other agent access.

## Required decision block

```text
ROUTING DECISION: DEFER TO: CODEX | ANTIGRAVITY
TASK TYPE: ...
COMPLEXITY SCORE: ... (estimated/confirmed)
REASON: ...
WHAT I INSPECTED: ...
WHAT REMAINS UNKNOWN: ...
```

## Antigravity → Codex implementation handoff

```text
CODEX TASK: <one bounded task>
GOAL: <observable outcome>
APPROVED DESIGN: <components, interfaces, data flow, constraints>
LIKELY FILES/AREAS: <known paths or clearly labeled estimates>
DO NOT CHANGE: <architecture or unrelated scope>
ACCEPTANCE CRITERIA: <checkable conditions>
VALIDATION: <test, scene, or CLI checks>
DEPENDENCIES / ORDER: <if any>
OPEN QUESTIONS: none, or list questions that must be resolved first
```

For large features, create an ordered list of small handoffs and wait for the user to return implementation results before reviewing. Do not assume the Codex task was completed.

## Codex → Antigravity design handoff

```text
ANTIGRAVITY TASK: design/specify <feature>
USER GOAL: <requested outcome>
PROJECT EVIDENCE: <relevant systems/files inspected>
ARCHITECTURE QUESTIONS: <decisions required>
CONSTRAINTS: <known limits>
REQUIRED OUTPUT: <implementation-ready specification and acceptance criteria>
CODEX STATUS: no files changed
```

## Codex → Antigravity diagnosis handoff

Include reproduction steps, exact error/log text, expected vs actual result, systems involved, steps already tried, evidence inspected, and ask for a diagnosis/plan. Do not claim the diagnosis is confirmed unless evidence supports it.
