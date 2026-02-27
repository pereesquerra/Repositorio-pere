# CLAUDE.md

This file provides guidance for AI assistants (Claude and others) working in this repository.

## Repository Status

This repository is currently **empty** — no source code, tests, or configuration files have been committed yet. This CLAUDE.md serves as the initial scaffolding document to establish conventions and workflows before development begins.

When the project is initialized, update the sections below with accurate, project-specific details.

---

## Repository Overview

| Field        | Value                                             |
|--------------|---------------------------------------------------|
| Repository   | pereesquerra/Repositorio-pere                     |
| Remote URL   | http://local_proxy@127.0.0.1:44222/git/pereesquerra/Repositorio-pere |
| Current Phase | Initial setup                                    |
| Language     | TBD                                               |
| Framework    | TBD                                               |

---

## Git Workflow

### Branch Naming

- Feature branches: `feature/<short-description>`
- Bug fix branches: `fix/<short-description>`
- AI-generated branches: `claude/<description>-<session-id>`
- Documentation branches: `docs/<short-description>`

### Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>(<scope>): <short summary>

<optional body>

<optional footer>
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `ci`

**Examples:**
```
feat(auth): add JWT token refresh logic
fix(api): handle null response from upstream service
docs: update CLAUDE.md with project structure
chore: add .gitignore for Node.js project
```

### Push Protocol

- Always push with tracking: `git push -u origin <branch-name>`
- AI branches must follow: `claude/<description>-<session-id>` (pushes to other branch patterns may fail)
- On network failure, retry up to 4 times with exponential backoff: 2s, 4s, 8s, 16s

---

## Development Workflow

### Before Starting Work

1. Pull the latest changes from the target branch
2. Create a new branch following the naming convention above
3. Understand the existing structure before making changes

### Making Changes

1. Read files before editing them — do not guess at file contents
2. Prefer editing existing files over creating new ones
3. Keep changes focused and minimal (avoid over-engineering)
4. Do not add comments, docstrings, or type annotations to code you didn't modify

### Completing Work

1. Run all tests before committing (commands TBD once project is initialized)
2. Run the linter/formatter before committing
3. Write clear commit messages
4. Push to the feature branch and open a pull request

---

## Project Structure (TBD)

This section should be updated once the project is initialized. A typical structure might look like:

```
Repositorio-pere/
├── CLAUDE.md           # This file
├── README.md           # Human-facing documentation
├── .gitignore          # Git ignore rules
├── src/                # Source code
├── tests/              # Test files
├── docs/               # Documentation
└── <config files>      # Language/framework-specific config
```

---

## Key Commands (TBD)

Update this section with the actual commands once the project is set up.

```bash
# Install dependencies
<command>

# Run the development server
<command>

# Build for production
<command>

# Run tests
<command>

# Run linter
<command>

# Run formatter
<command>
```

---

## Coding Conventions (TBD)

Once the project language and framework are chosen, document conventions here:

- **Language version:** TBD
- **Formatting tool:** TBD
- **Linting tool:** TBD
- **Test framework:** TBD
- **Code style:** TBD

---

## Environment Variables

Document required environment variables here once the project is initialized.

```
# Example:
# DATABASE_URL=<connection string>
# API_KEY=<secret key>
```

Never commit secrets or `.env` files containing real credentials.

---

## Testing Guidelines (TBD)

- Test files should live alongside source files OR in a dedicated `tests/` directory
- All new features should include tests
- All bug fixes should include a regression test
- Aim for meaningful coverage, not just high numbers

---

## CI/CD (TBD)

Document any CI/CD pipelines configured for this repository (GitHub Actions, GitLab CI, etc.) once set up.

---

## Notes for AI Assistants

- This repository is empty — do not assume any file exists without checking first
- When the project is initialized, update all "TBD" sections with accurate information
- Always read files before modifying them
- Confirm before taking destructive or irreversible actions (force push, dropping tables, deleting branches)
- Keep changes focused on what was requested — avoid unsolicited refactoring or "improvements"
- Do not push to branches other than the one designated in your task
