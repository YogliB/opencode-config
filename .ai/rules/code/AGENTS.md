# Coding Rules

## Purpose

Ensure code is clear, consistent, and self-explanatory — no inline comments needed.

## Core Principle

Never explain code with comments.  
If explanation feels necessary, rewrite for clarity.

## Guidelines

- Use **intention-revealing names** for variables, functions, and types.
- Keep functions **small, focused, and testable**.
- Prefer **simple control flow** — early returns, clear conditionals.
- Let **types and tests** express intent and constraints.
- Document design rationale in markdown files, not source code.
- Follow **Clean Code**: readable, maintainable, minimal cognitive load.

### Clean Code Checklist

- **SRP:** one purpose per function/module.
- **DRY:** no duplicated logic.
- **KISS:** simple > clever.
- **Pure Functions:** avoid side effects.
- **Meaningful Names:** reflect purpose.
- **Consistent Style:** format uniformly.
- **Fail Fast:** validate early.
- **Readable > Optimal:** clarity first.

## Naming Conventions

- **Functions:** verbs → `fetchUserProfile`
- **Types/Classes:** nouns → `RetryPolicy`
- **Clarity over brevity:** `timeoutMs` > `t`, `maxRetries` > `mr`
- **Include units/context:** `cacheDurationSeconds`, `fileSizeBytes`

## Allowed Comments

- Auto-generated headers or licenses only — minimal and standardized.

## Forbidden Comments

- No inline comments (`// explanation` or `# explanation`)
- No docstrings (`"""docstring"""` or `/** JSDoc */`)
- No TODO, FIXME, or similar markers
- No explanations, rationales, or descriptions in any form

---

**Summary:**  
Code should explain itself through naming, structure, and typing.  
Follow **Clean Code** for clarity, simplicity, and long-term maintainability.
