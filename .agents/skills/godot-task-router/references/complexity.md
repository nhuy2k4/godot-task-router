# Complexity and risk rubric

Score from evidence in the request and repository. Estimates are allowed but must be labeled estimates. Count overlapping criteria separately only when they represent distinct impacts; explain the reason for each point.

## Add points

| Signal | Points |
|---|---:|
| Estimated change spans 2–4 existing files | +1 |
| Estimated change spans 5+ existing files | +2 (use instead of +1) |
| Touches 2 game systems | +1 |
| Touches 3+ systems | +2 (use instead of +1) |
| Introduces a new system/subsystem | +2 |
| Requires a new data model or Resource design | +1 |
| Requires architectural decisions or changes current architecture | +2 |
| Changes save data, migration, or persistence behavior | +2 |
| Affects multiplayer/network protocol or synchronization | +2 |
| Requires gameplay and UI coordination | +1 |
| Requirements are materially ambiguous | +1 |
| Several viable technical approaches have meaningful tradeoffs | +1 |
| Requires research into an unfamiliar Godot API/plugin | +2 |
| Bug source is unknown after relevant inspection | +2 |
| Bug spans multiple systems | +2 |
| Material platform, performance, data-loss, or compatibility risk | +2 |

Do not add a file-count point for a pure mechanical rename by itself when architecture and behavior stay unchanged; explain the actual scope instead.

## Score bands

- **0–2, simple:** Codex can implement a clear, local change.
- **3–5, normal:** Codex can implement if the design and acceptance criteria are clear. If the work introduces architecture choices, defer to Antigravity despite the score.
- **6–8, complex:** Antigravity should analyze/design and break down work first; Codex implements approved subtasks.
- **9+, major:** Antigravity specification → Codex implementation and validation → Antigravity review.

## Escalation overrides

Always route to Antigravity first, regardless of score, when the request: introduces a core game system; changes existing architecture; changes save format/migration; changes multiplayer architecture/protocol; adds an autoload/global service; requires more than three systems to interact; or is foundationally ambiguous such that different choices produce different architectures.

## Uncertainty rule

If complexity is unclear, inspect the relevant project files read-only and recalculate. If it remains unclear, return `NEEDS CLARIFICATION` or defer to Antigravity. Never fabricate exact file counts or claim a complete audit from a partial inspection.

## Model guidance (advisory only)

Model choice is a separate decision from agent ownership. Use fast reasoning for mechanical/local edits, ordinary reasoning for normal implementation, and stronger reasoning for architecture, cross-system debugging, or high-risk refactors. The skill cannot change a model or quota in another application; the user selects the model there.
