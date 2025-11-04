# 🧩 MCP Tools Rules

## Overview

These rules define **how the agent interacts with external MCP servers** for data retrieval, automation, and reasoning tasks.
All tools listed below are automatically available through the configured MCP servers.

---

## 🔧 General Rules

1. **Always prefer local knowledge first** — use MCP tools **only when information or execution cannot be done natively.**
2. **Explain the reasoning briefly** before invoking an MCP (e.g., “using `fetch` to get remote content…”).
3. **Do not repeat tool descriptions** — focus on intent and relevant arguments.
4. **If multiple MCPs overlap**, use the one most specific to the user’s intent (priority order below).

---

## ⚙️ Priority Order

1. **gh_grep** → for GitHub code/content queries.
2. **figma** → for design or UI resource access.
3. **fetch** → for generic remote data (HTTP, JSON, text retrieval).
4. **playwright** → for browser automation, UI testing, or page state capture.
5. **sequentialthinking** → for structured reasoning, long-chain tasks, or sequential workflow planning.

---

## 📡 Tool Usage Guidelines

### 1. `fetch`

- **Purpose:** Retrieve remote content (APIs, docs, JSON, etc.).
- **Invocation:** Use for HTTP GET/POST tasks not covered by other MCPs.
- **Rules:**

  - Always specify full URL and headers if required.
  - Prefer structured responses (JSON/YAML) over raw HTML.
  - Cache or summarize large responses before further use.

---

### 2. `figma`

- **Purpose:** Access local Figma MCP service (`http://127.0.0.1:3845/sse`).
- **Usage:**

  - For design inspection, layout documentation, and design token extraction.
  - When synced with internal Cursor docs, annotate retrieved data for doc alignment.

---

### 3. `gh_grep`

- **Purpose:** Query codebases or repositories remotely using grep.app’s API.
- **Usage:**

  - Use precise query strings (regex or keyword-based).
  - Return minimal snippets unless full file context is explicitly needed.

- **Rule:** Never commit or modify code directly based on grep results without review.

---

### 4. `playwright`

- **Purpose:** Automate browser interaction, scrape DOMs, run headless testing.
- **Rules:**

  - Use only for deterministic UI or rendering workflows.
  - Avoid heavy crawling or dynamic pages unless explicitly required.
  - Summarize results for docs or debugging purposes.

---

### 5. `sequentialthinking`

- **Purpose:** Chain logical steps across multi-turn reasoning or dependent tasks.
- **Usage:**

  - Ideal for “plan → simulate → evaluate” workflows.
  - When integrated with docs sync, attach outputs as reasoning logs or process trees.

---

## 🧠 Internal Docs Integration

- The agent must **sync all relevant tool outputs** to Cursor’s internal documentation when:

  - New insight, architecture note, or debugging trace is generated.
  - Any MCP output contributes to the project’s evolving knowledge base.

- Include a short **Context Header** (timestamp + tool name + summary) for traceability.

**Example:**

> [MCP: fetch | 2025-11-02 | Retrieved API spec from example.com]

---

## 🧩 Error Handling

- If a tool fails or returns an unexpected format:

  - Retry **once** with simplified parameters.
  - If failure persists, fall back to natural-language summarization or ask for clarification.

---

## 🧱 Extensibility

When adding a new MCP:

- Append under “📡 Tool Usage Guidelines” with a consistent structure.
- If it replaces an existing one, note the deprecation in the header.
- Update priority order to reflect scope and reliability.

---

## ✅ Quick Summary

| Tool                 | Role              | Typical Use                  |
| -------------------- | ----------------- | ---------------------------- |
| `fetch`              | Generic retrieval | Fetch remote JSON/docs       |
| `figma`              | Design interface  | Inspect layouts, sync tokens |
| `gh_grep`            | Code search       | Query repos and codebases    |
| `playwright`         | Automation        | Headless browser testing     |
| `sequentialthinking` | Reasoning         | Plan or simulate workflows   |
