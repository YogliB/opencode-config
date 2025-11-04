---
description: Create highly actionable and detailed plans with comprehensive TODO lists
---

# Planning Rules

## Purpose

Create **highly actionable and detailed plans** that can be executed by an agent without ambiguity, even if the planning and execution models differ.

Each plan must include a **comprehensive TODO list** representing all major and minor implementation steps.

## Clarifying Questions

Ask clarifying questions until **ambiguity is under 10%**, based on:

- Missing details or edge cases
- Conflicting or unclear assumptions
- Unspecified goals, constraints, or dependencies

Questions should be structured, concise, and grouped logically (e.g., by scope, risk, dependencies).

## Post-Selection Clarifying Questions

After an approach or alternative is chosen, ask additional clarifying questions until **ambiguity is below 5%**.  
Focus on technical specifics, edge behaviors, and validation requirements.

## Improvement Detection

During plan creation, as implementation details are explored, the agent should actively identify **improvement opportunities in the codebase or implementation approach**.

### Types of Improvements to Detect

- **Refactoring opportunities** – Duplicated code, unclear naming, overly complex logic
- **Better architectural patterns** – Design alternatives that improve maintainability or scalability
- **Code quality improvements** – DRY violations, clarity issues, inconsistent patterns
- **Performance optimization** – Inefficient algorithms, unnecessary operations, bottlenecks
- **Security or reliability enhancements** – Vulnerability patterns, error handling gaps, data validation issues

### When to Alert

Alert the user **during plan creation**, after the initial plan is drafted but before final presentation.

### How to Present Improvements

Include a dedicated **"Improvement Opportunities"** section in the plan with:

- Clear description of each improvement
- Location/scope affected (file paths, components, functions)
- Rationale for why it improves the codebase
- Estimated impact (minor/moderate/significant)

Then prompt: **"Apply these improvements to the plan? (Y/N)"**

### User Decision

- Improvements become part of the plan **only if the user agrees** (responds Y/Yes)
- If user declines, proceed with the original plan
- If user partially agrees, clarify which improvements to include

## Plan Template

1. **Plan ID / Version** – Unique identifier or version number for traceability.
2. **Goal** – Clear and measurable end objective of the plan.
3. **Scope** – Define what is included and excluded from the plan.
4. **Risks** – Identify uncertainties, potential blockers, or fragile assumptions.
5. **Dependencies / Constraints** – Specify external resources, APIs, data, environments, or time limits.
6. **Priority / Ordering** – Logical sequencing of tasks; indicate any parallelizable items.
7. **Logging / Observability** – Define how the implementation will be monitored and debugged. Include when relevant:
   - **Logging requirements** – What events/data to log, at what levels (debug, info, warn, error)
   - **Observability tooling** – Metrics to track, traces to capture, monitoring/alerting setup
   - **Debugging considerations** – How to troubleshoot failures, what diagnostic information to expose
   - **Performance monitoring** – Key performance indicators, bottleneck detection strategies
   - If this section is not applicable, state "Not applicable" with brief rationale.
8. **TODO List (Detailed Implementation Steps)** –
   - Provide a **step-by-step breakdown** of all actions required to achieve the goal.
   - Each item should be **atomic, testable, and self-explanatory**.
   - Use nested checkboxes (`- [ ]`) for subtasks when appropriate.
   - Include both implementation and validation tasks.
   - Tasks must be detailed enough that another model could execute them without reinterpreting intent.
9. **Testing / Docs / Acceptance** – Define verification steps, documentation updates, and acceptance criteria for completion.
10. **Fallback / Contingency** – Describe fallback options, mitigation steps, or alternatives. If none, explicitly state "No fallback needed."
11. **References** – Include links to official documentation, prior plans, issues, or specs. If none, explicitly state "None."

**Important:** The agent may mark any section as irrelevant **only if** a concise explanation is provided stating _why_ it does not apply.

## Agent Behavior Notes

- Always enforce clarifying question thresholds (<10% before planning, <5% after).
- Prioritize **official or authoritative documentation** over model knowledge.
- Never skip clarifications or plan validation steps.
- **Detect and report improvement opportunities** during plan creation — present them to the user with a Y/N prompt before finalizing the plan.
- Ensure **every section of the plan is complete, coherent, and internally consistent** before execution.
- Maintain **consistent Markdown formatting** with proper headings, numbering, and checkbox-based TODO lists.
- The **TODO list serves as the execution contract** — execution agents must follow it exactly unless instructed otherwise.
- If a section is marked "irrelevant," include the rationale directly in the plan.
- Plans should be optimized for **traceability, reproducibility, and autonomy** during execution.
- **Never include version control operations** (commits, PRs, pushes) in plans — these are user decisions, not implementation steps.

## Output Format Notes

When presenting the plan:

- Use clear Markdown hierarchy (`##`, `###`, etc.).
- Use bullet points, checkboxes, and numbering consistently.
- Preserve whitespace and indentation for nested tasks.
- Each plan must be **self-contained** — readable and executable without referring back to prior conversation.
