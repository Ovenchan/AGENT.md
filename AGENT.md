# AGENT.md

## Purpose

This document defines how the coding agent should work in this repository.

The agent should prioritize clarity, small safe iterations, and practical debugging over overengineering.

---

## Working Style

### 1. Plan before coding

Before making any code changes, the agent must first provide a brief implementation plan.

The plan should include:
- the goal of the task
- the files or modules likely to be touched
- the intended approach
- any assumptions or uncertainties
- the order of execution

The plan should be concrete and actionable, not generic.

Do not start coding immediately unless the task is trivial.

---

### 2. Keep the project simple and engineering-oriented

The agent should keep the project structure clean, readable, and maintainable.

Prefer:
- simple module boundaries
- clear naming
- minimal abstractions
- implementation that matches the current scale of the project

Avoid:
- unnecessary wrappers
- speculative abstractions
- excessive fallback logic
- defensive code for scenarios that are not currently relevant
- premature optimization

The code should be engineered, but not overengineered.

---

### 3. Ask about unclear implementation details

If important implementation details are ambiguous, the agent should ask for clarification before proceeding.

When asking, the agent should not ask vague questions.  
Instead, it should present a small set of feasible options and explain the trade-offs briefly.

For example:
- Option A: simpler and faster to implement
- Option B: cleaner for future extension
- Option C: closer to current architecture

When presenting multiple options, the agent should explicitly recommend one default choice unless the user asks for a neutral comparison.

Then wait for the user's choice if the ambiguity is substantial.

If the ambiguity is minor, the agent may make a reasonable assumption, but must state it explicitly before coding.

---

### 4. Debug based on actual results

The agent should rely on real execution results, logs, and error messages to debug issues.

Prefer:
- reproducing the issue
- locating the exact failing step
- making targeted fixes
- verifying the fix after changes

Avoid:
- adding large amounts of fallback code without evidence
- guessing root causes without checking the runtime behavior
- masking errors instead of solving them

The agent should use observed behavior to drive debugging.

---

### 5. Review after implementation

After coding, the agent must perform a brief review.

The review should include:
- what was changed
- why the change solves the problem
- possible risks or edge cases
- whether further cleanup or testing is recommended

If something is still uncertain, the agent should say so clearly.

---

## Execution Rules

### 6. Prefer small, traceable changes

Make small and understandable edits whenever possible.

Do not rewrite large parts of the project unless necessary.

If a larger refactor is truly needed, explain why the smaller alternative is insufficient before proceeding.

Prefer changes that are easy to review. Avoid touching unrelated files in the same iteration.

---

### 7. Respect the existing architecture

Unless the user explicitly requests otherwise, the agent should work with the current project structure and conventions.

Do not introduce:
- new frameworks
- major directory reshuffling
- broad naming changes
- large-scale refactors

unless they are justified by the task.

---

### 8. Be explicit about assumptions

If the agent makes assumptions, it must state them clearly.

Assumptions should be separated from confirmed facts.

Do not present guesses as if they were confirmed requirements.

---

### 9. Keep interfaces stable

Do not change public interfaces, file formats, or function signatures unless necessary.

If such changes are needed, explain the impact first, including:
- what will change
- why the change is necessary
- which parts of the project may be affected
- whether migration or follow-up edits are needed

Prefer internal implementation changes over external interface changes when both can solve the task.

---

### 10. Testing should be practical

Testing should match the scale of the task.

For small fixes:
- run the relevant part
- verify the failing case
- confirm no obvious regression

For larger changes:
- suggest a minimal but meaningful validation plan

Do not create excessive test scaffolding unless the project already expects it or the user asks for it.

---

## Communication Format

### 11. Suggested response flow

For non-trivial tasks, the agent should usually respond in this order:

1. Plan  
2. Questions or options (if needed)  
3. Implementation  
4. Validation / debugging result  
5. Review

This keeps the workflow predictable and transparent.

---

### 12. When presenting options

When multiple implementation paths exist, the agent should provide a short comparison.

Each option should include:
- what it does
- main benefit
- main drawback
- recommended choice

Keep this concise.

---

### 13. When blocked

If blocked by missing requirements, missing files, or conflicting constraints, the agent should:

- explain the exact blocker
- identify what is known and unknown
- propose the most reasonable next options

Do not continue with hidden assumptions when the missing detail is critical.

---

## Decision Priorities

When there is a trade-off, use this priority order:

1. Correctness
2. Clarity
3. Simplicity
4. Compatibility with existing code
5. Extensibility
6. Performance optimization

Unless the user explicitly asks otherwise, do not sacrifice clarity and simplicity for speculative flexibility.

---

## What the agent should avoid

The agent should avoid:
- coding before planning
- making large hidden assumptions
- overengineering
- excessive boilerplate
- adding fallback branches without evidence
- changing unrelated files
- broad refactors without approval
- claiming a fix without validation
- skipping review after implementation

---

## Definition of Done

A task is considered complete only when:

- a plan was provided first
- unclear details were clarified or explicitly assumed
- the code change was implemented
- the result was checked through execution, reasoning, or targeted validation
- a brief review was provided

---

## Default Behavior

If no special instruction is given, the agent should act as follows:

- plan first
- ask when key details are unclear
- recommend a default option when multiple feasible approaches exist
- implement with minimal necessary complexity
- keep public interfaces stable unless change is necessary
- prefer small, reviewable edits
- debug from actual runtime evidence
- review the result before concluding