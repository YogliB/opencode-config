# Before PR Command

**Purpose:**  
Run this command before creating a pull request to ensure the current feature branch is clean and any issues are fixed. The agent will automatically detect the project type and run the appropriate validation commands.

**Commands:**

The agent will detect the project type and run the appropriate commands:

**For UI Projects** (detects `package.json`):

```bash
npm run verify
npm run test:ci:unit:coverage
```

**For Backend Python Projects** (detects `pyproject.toml`):

```bash
poetry run cybr pr
poetry run bandit
```

**Instructions:**

- Run this on your **current feature branch** (not main/master).
- The agent will automatically detect project type based on configuration files.
- Commands run sequentially and stop on first failure.
- **DO NOT create a PR** - only run checks and fix reported issues.

**What each command checks:**

**UI Projects:**

`npm run verify`:
- Linting (ESLint)
- Code formatting (Prettier)
- Style linting (Stylelint for SCSS/CSS)

`npm run test:ci:unit:coverage`:
- Unit tests with coverage
- Test results and coverage reports

**Backend Python Projects:**

`poetry run cybr pr`:

- Pre-commit hooks (YAML, JSON, TOML formatting, trailing whitespace, etc.)
- Import sorting (isort)
- Code formatting (black)
- Code complexity analysis (radon, xenon)
- Linting (pylint)

`poetry run bandit`:

- Security vulnerability scanning
- Common security issue detection
- Best practice violations

- Fix any reported issues before proceeding to open a PR.
- After successful execution of all checks, your branch should be ready for a pull request.

**Expected Output:**

**For UI Projects:**

- All ESLint checks pass
- All files properly formatted (Prettier)
- All style linting checks pass (Stylelint)
- All unit tests pass with coverage
- Clean console output with no warnings or errors

**For Backend Python Projects:**

- All pre-commit checks pass
- Code rating should be close to 10/10
- Any auto-fixes (like import sorting) will be applied automatically
- No security vulnerabilities detected by bandit
- All commands complete with exit code 0
