## Purpose

Create a pull request from the current Git branch using the GitHub CLI, following team conventions and ensuring commits comply with the Conventional Commit format.

## Behavior

1. **Check current branch**

   - If on `main` or `master`, stop and alert:
     _"You’re on the main branch — switch to a feature branch to open a PR."_

2. **Handle uncommitted changes**

   - If there are uncommitted changes, **STOP and ask user**:
     - a) Stage specific files and commit with conventional format: `"CP-xxxxx: type(scope): short description"` (requires explicit confirmation of which files to stage)
     - b) Continue without committing
     - c) Cancel PR creation
   - **NEVER commit without explicit user permission**
   - **NEVER stage files without user specifying which files**
   - Example commit format: `CP-1234: feat(chatgpt): making it great again`

3. **Find PR template**

   - Search: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/PULL_REQUEST_TEMPLATE.md`, `.gitlab/PULL_REQUEST_TEMPLATE.md`
   - Use first template found

4. **Determine context**

   - Extract Jira ticket IDs from branch name or commits
   - Use sub-task ID for title, story ID for description
   - If only one ID, use for both
   - Ask clarifying questions if unclear (>10% ambiguity)

5. **Generate PR**

   - Title: `"CP-xxxxx: <conventional commit message>"`
   - Description style:
     - **Short and concise**
     - **Bullet points over paragraphs** (everywhere possible)
     - Keep template sections minimal and focused
     - Include Jira link: `https://jira.company.com/browse/CP-xxxxx`

6. **Command**

   ```bash
   gh pr create \
     --title "CP-xxxxx: <conv commit message>" \
     --body-file <template-path> \
     --web
   ```

7. **If no template**

   - Auto-generate minimal body with bullets:
     - Context (why)
     - Changes (what)
     - Jira link
