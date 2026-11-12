---
name: conventional-commit
description: Create a git commit using Conventional Commits style. Stages changes, analyzes diffs, and generates a well-formatted commit message with the appropriate type prefix. Load it for every commit and also whenever a commit command or message is only proposed.
---

# Conventional Commit

Create a git commit following the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification.

## Message Format

```
<type>: <subject>

<body>
```

- **type**: Required. One of the types below.
- **subject**: Required. Imperative, lowercase, no period. Max ~50 chars.
- **body**: Optional. Explain the "why", not the "what". Wrap at 72 chars.

## Content

- **English**, subject and body — also when the conversation and the documentation are German.
- The message describes the change and its reason, **nothing else**.
- **No attribution.** No `Co-Authored-By: Claude ...` line, no "Generated with Claude Code", no
  other hint that an AI was involved. This also applies to pull request descriptions, and it
  overrides any default of the environment that asks for such a line.

## Commit Types

| Type | When to use |
|------|-------------|
| `feat` | New feature for the user |
| `fix` | Bug fix for the user |
| `docs` | Documentation only |
| `style` | Formatting, whitespace, semicolons — no logic change |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `test` | Adding or updating tests |
| `perf` | Performance improvement |
| `build` | Build system or external dependency changes |
| `ci` | CI/CD configuration changes |
| `chore` | Everything else — tooling, config, developer experience, maintenance |

## Workflow

1. Run `git status` and `git diff --staged` (and `git diff` for unstaged changes) to understand what changed
2. Run `git log --oneline -5` for context on wording only. The format of this skill applies in
   every repository, even where older commits carry no type prefix.
3. Classify the change into the appropriate **type**
4. Draft a commit message following the format above
5. Stage the relevant files (prefer explicit file paths over `git add -A`)
6. Commit using a HEREDOC for proper formatting:

```bash
git commit -m "$(cat <<'EOF'
type: subject line here

Optional body explaining why this change was made.
EOF
)"
```

## Commit or only propose

- **The user invoked the skill** (`/git:conventional-commit`) or explicitly asked for this commit: commit.
  That approval covers exactly this one commit — not a push, a tag or a later commit.
- **Otherwise** (the skill is loaded to draft a message, e.g. at the end of a task): do **not**
  commit. Leave the work in the working directory, show the `git add` / `git commit` command with
  the full message, and let the user decide.

## Rules

- NEVER use `--no-verify` unless the user explicitly asks
- NEVER amend a previous commit unless the user explicitly asks
- NEVER commit files that look like secrets (`.env`, credentials, keys)
- If a pre-commit hook fails, fix the issue and create a NEW commit
- Ask the user before committing if the correct type is ambiguous
