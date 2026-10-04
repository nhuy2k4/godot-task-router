# Godot Task Router

A rule set for **classifying tasks, assigning responsibilities, and handing work off between Antigravity and Codex** in a Godot project.

- **Antigravity**: focuses on design, architecture, analysis, task decomposition, research, and review.
- **Codex**: focuses on implementation, debugging, refactoring, testing, and verification.

The goal is to ensure that each AI agent only handles tasks that match its role, reducing duplicated work and avoiding the use of high-capability models for tasks that do not require them.

## Installation

Make sure the `Godot_Task_Router` files are placed in the root directory of your Godot project, at the same level as:

```text
project.godot
```

Recommended structure:

```text
project-root/
├── project.godot
├── AGENTS.md
├── TASK_HANDOFF_TEMPLATE.md
└── .agents/
    └── skills/
        └── godot-task-router/
            ├── SKILL.md
            └── references/
```

If your project already has an `AGENTS.md` file, merge the rules from this package into the existing file instead of overwriting it.

Keep the following path unchanged:

```text
.agents/skills/godot-task-router/
```

This is the project-level skill location used by Antigravity for skill discovery. Codex may also use the skill in environments that support Agent Skills.

If the skill does not appear after adding it to the project, reopen your workspace or IDE.

You can also explicitly instruct the agent to use it:

```text
/godot-task-router
```

or:

```text
Read the godot-task-router skill before handling this task.
```

## Structure

### `AGENTS.md`

Project-level instructions that require the agent to **classify the task before starting work**.

The agent should determine one of the following outcomes:

```text
ACCEPT
```

or:

```text
DEFER TO ANTIGRAVITY
```

or:

```text
DEFER TO CODEX
```

before implementation begins.

---

### `.agents/skills/godot-task-router/SKILL.md`

This is the core of the system.

The skill contains:

- Task classification workflow.
- Responsibility split between Antigravity and Codex.
- `ACCEPT / DEFER` rules.
- Task complexity evaluation.
- Rules for unclear or ambiguous tasks.
- Handoff workflow.
- Large-feature workflow.
- Review and escalation rules.

---

### `references/`

Contains supporting documentation for the skill, including:

- Complexity rubric.
- Role definitions.
- Handoff rules.
- Task classification examples.
- Special-case scenarios.

Agents can consult these references when additional information is needed before making a routing decision.

---

### `TASK_HANDOFF_TEMPLATE.md`

A template used to transfer work between Antigravity and Codex.

A handoff may contain:

- Objective.
- Scope.
- Relevant architecture.
- Files to modify.
- Constraints.
- Acceptance criteria.
- Required tests.
- Known issues.
- Open questions.

The template helps the receiving agent continue work without having to re-analyze the entire project from scratch.

## How It Works

### When Codex receives a task

Codex should generally `ACCEPT` tasks such as:

- Implementing a feature with an existing specification.
- Writing GDScript.
- Fixing bugs with a clearly defined scope.
- Refactoring code.
- Writing unit or integration tests.
- Running tests.
- Fixing build errors.
- Making small scene or script changes.
- Optimizing code within a clearly defined scope.

Codex should:

```text
DEFER TO ANTIGRAVITY
```

when the task involves:

- Architecture design.
- A core feature without an existing specification.
- System structure decisions.
- Choosing design patterns.
- Large gameplay system design.
- Analysis across multiple subsystems.
- Changes with a large blast radius.
- Ambiguous requirements.
- Multiple valid implementation directions requiring design decisions.

---

### When Antigravity receives a task

Antigravity should generally `ACCEPT` tasks such as:

- Architecture design.
- Requirement analysis.
- Breaking large features into smaller tasks.
- Gameplay system design.
- Research.
- Implementation review.
- Investigating complex bugs.
- Dependency analysis.
- Writing implementation plans.
- Writing specifications.
- Risk analysis.

Antigravity should:

```text
DEFER TO CODEX
```

when the task mainly involves:

- Implementing code from an existing specification.
- Fixing simple bugs.
- Performing clearly defined refactors.
- Writing tests.
- Direct file modifications.
- Mechanical implementation work.

## Recommended Workflow

For small features:

```text
Task
 ↓
Router
 ↓
Codex
 ↓
Implement + Test
```

For large features:

```text
Task
 ↓
Antigravity
 ↓
Analyze / Design
 ↓
Spec + Handoff
 ↓
Codex
 ↓
Implement + Test
 ↓
Antigravity
 ↓
Review
```

Example:

```text
User:
"Create an inventory system for the game."

Antigravity:
1. Analyze requirements.
2. Design the data model.
3. Define InventoryManager.
4. Define Item Resource.
5. Design save/load behavior.
6. Break implementation into tasks.
7. Create the handoff.

        ↓

Codex:
1. Read the handoff.
2. Implement the system.
3. Write tests.
4. Run the project/tests.
5. Report the result.

        ↓

Antigravity:
1. Review the implementation.
2. Check the architecture.
3. Verify requirements.
4. Suggest changes if necessary.
```

## Routing Decision

Before working on a task, the agent should display its routing decision.

Example:

```text
ROUTING DECISION

Agent: Codex
Decision: ACCEPT
Complexity: Medium
Reason: The feature already has a clear specification and mainly requires implementation.
```

Or:

```text
ROUTING DECISION

Agent: Codex
Decision: DEFER TO ANTIGRAVITY
Complexity: High
Reason: The task requires architectural decisions across multiple subsystems and does not yet have an implementation plan.
```

This allows the user to verify that the correct agent is handling the correct type of task before any project files are modified.

## Handoff Between Antigravity and Codex

The skill **does not automatically send tasks between applications or accounts**.

The current workflow is:

```text
Antigravity
    ↓
TASK_HANDOFF
    ↓
User transfers the task
    ↓
Codex
```

And in the opposite direction:

```text
Codex
    ↓
Implementation Result
    ↓
User transfers the result
    ↓
Antigravity Review
```

In the future, this workflow could be combined with:

- MCP.
- GitHub Issues.
- GitHub Pull Requests.
- Shared task files.
- Automation scripts.
- Agent orchestration.

to reduce the amount of manual task transfer.

## Important Principles

The router is an **orchestration rule set**, not a security system or sandbox.

Agents may still occasionally fail to follow instructions perfectly.

Before allowing an agent to make large changes, check its:

```text
ROUTING DECISION
```

to make sure the correct agent is handling the appropriate type of work.

General rule:

```text
THINK / DESIGN / PLAN / REVIEW
        ↓
   ANTIGRAVITY

IMPLEMENT / FIX / TEST
        ↓
      CODEX
```

If a task requires both design and implementation:

```text
ANTIGRAVITY
    ↓
SPEC
    ↓
CODEX
    ↓
IMPLEMENT
    ↓
ANTIGRAVITY
    ↓
REVIEW
```

This is the default workflow of **Godot Task Router**.