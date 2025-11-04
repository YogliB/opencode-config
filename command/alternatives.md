---
description: Suggest viable alternative approaches for code, plans, or designs
---

## Purpose

Suggest **viable alternative approaches** for the given context — code, plan, or design.
Encourage exploration before committing to a single direction.

## Behavior

1. Present **up to 3** realistic and context-appropriate alternatives.

   - Each includes:

     - **Idea:** concise description
     - **Snippet:** minimal illustrative example (if relevant)
     - **Pros / Cons:** short, balanced summary

2. Provide **1 clear recommendation**, based on clarity, maintainability, and context.
3. **Stop after presenting** — wait for user selection before continuing.
4. **Never produce diffs or file edits.**
5. Ask clarifying questions only if uncertainty >10%.

### Example Output

**Option 1: Use a shared helper function**

- **Idea:** Extract common logic into a reusable utility function
- **Snippet:**
  ```typescript
  function processData(data: Data[]) {
    return data.filter(validateEntry).map(transformEntry);
  }
  ```
- **Pros:**
  - DRY
  - Consistent
- **Cons:**
  - Slightly more indirection

**Recommendation:** Option 1 — best balance of simplicity and reuse.
