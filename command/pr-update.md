---
description: Update existing pull request title and description using GitHub CLI
---

## Purpose

Update an existing pull request's title and description to reflect the current branch state, using the GitHub CLI and following team conventions. Smart merge preserves manual additions while regenerating template sections with current data.

## Behavior

1. **Check current branch**

   - If on `main` or `master`, stop and alert:
     _"You're on the main branch — switch to a feature branch to update a PR."_

2. **Handle uncommitted changes**

   - If there are uncommitted changes, **STOP and ask user**:
     - a) Stage specific files and commit with conventional format: `"CP-xxxxx: type(scope): short description"` (requires explicit confirmation of which files to stage)
     - b) Continue without committing
     - c) Cancel update
   - **NEVER commit without explicit user permission**
   - **NEVER stage files without user specifying which files**

3. **Find PR to update**

   - Always prompt for PR number
   - Validate PR exists: `gh pr view <number> --json number,headRefName`
   - Confirm PR belongs to current branch
   - Stop if validation fails

4. **Find PR template**

   - Search: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/PULL_REQUEST_TEMPLATE.md`, `.gitlab/PULL_REQUEST_TEMPLATE.md`
   - Use first template found

5. **Determine context**

   - Extract Jira ticket IDs from branch name or commits
   - Use sub-task ID for title, story ID for description
   - If only one ID, use for both
   - Ask clarifying questions if unclear (>10% ambiguity)

6. **Smart merge description**

   - Fetch existing PR body: `gh pr view <number> --json body`
   - Identify template sections vs manual content
   - Regenerate template sections with current data
   - Preserve non-template content (manual additions)
   - If uncertain about merge conflicts, show diff and ask user

7. **Update PR**

   - Title: `"CP-xxxxx: <conventional commit message>"`
   - Description style:
     - **Short and concise**
     - **Bullet points over paragraphs** (everywhere possible)
     - Keep template sections minimal and focused
     - Include Jira link: `https://jira.company.com/browse/CP-xxxxx`

8. **Command**

   ```bash
   gh pr edit <number> \
     --title "CP-xxxxx: <conv commit message>" \
     --body "<merged-content>"
   ```

9. **If no template**

   - Preserve existing description structure
   - Only update Jira links and key sections
   - Auto-generate minimal body with bullets:
     - Context (why)
     - Changes (what)
     - Jira link
