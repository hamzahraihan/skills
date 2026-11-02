---
name: git-micro-commit
description: 'Use this skill when the user wants to make micro commits: tiny, single-purpose commits of one file or one small logical change at a time. Stages a minimal file set, writes a short Conventional Commits message, runs git commit, and repeats for each change. Do not use it to push, open a pull request, rebase, or rewrite history.'
license: MIT
compatibility: 'Requires Git.'
allowed-tools: shell(git:*)
---

# Micro Commits

Make tiny Git commits — one file or one small logical change per commit — following the [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) specification. Each commit is a single, reviewable unit.

## Message Format

```text
<type>: <summary>
```

Micro commits keep the message minimal: type, optional scope, one-line imperative summary. Body and footer only when genuinely needed (for example a linked issue).

```text
fix(parser): accept empty input

Closes: #123
```

- Keep the first line at 72 characters or less. No period at the end.
- Write the summary in the imperative mood: "add", not "added" or "adds".
- Without a scope: `<type>: <summary>`.

## Types

Conventional Commits defines only `feat` and `fix`. The other types come from the Angular convention. If the repository has its own list (commitlint config, `CONTRIBUTING.md`, recent `git log`), use that list.

| Type       | Use it for                                     |
| ---------- | ---------------------------------------------- |
| `feat`     | A new feature                                  |
| `fix`      | A bug fix                                      |
| `docs`     | Documentation only                             |
| `style`    | Formatting only, no logic change               |
| `refactor` | A code change that is not a feature or fix     |
| `perf`     | A performance improvement                      |
| `test`     | New or changed tests                           |
| `build`    | The build system or dependencies               |
| `ci`       | CI configuration                               |
| `chore`    | Other maintenance                              |
| `revert`   | A revert of an earlier commit                  |

## Workflow

### 1. Read the repository rules

- Commitlint config (for example `commitlint.config.js`, `.commitlintrc.json`).
- `CONTRIBUTING.md`.
- Recent messages: `git log --oneline -10`.

If a repository rule differs from this skill, use the repository rule.

### 2. Examine the changes

```bash
git status --porcelain
git diff
```

If there are no changes, tell the user. Do not make an empty commit.

### 3. Pick the smallest logical change

A micro commit touches one file, or one tight cluster of files that cannot be understood separately (for example a component and its test). Do not bundle unrelated changes.

```bash
git diff -- path/to/file
```

Decide the type and scope from that single diff.

### 4. Stage only those files

```bash
git add -- path/to/file1 path/to/file2
```

- Put globs in quotes: `git add -- '*.test.*'`.
- Never use `git add -p` or `git add -i` (they wait for a person).
- After resolving a merge conflict: `git add --resolved`.

Check what is staged:

```bash
git diff --staged --name-only
git diff --staged --stat
```

Never commit secrets (`.env`, `credentials.json`, private keys).

### 5. Commit

One `-m` per paragraph; Git inserts blank lines between them:

```bash
git commit -m "fix(parser): accept empty input"
git commit -m "docs(readme): add setup section" -m "Closes: #123"
```

For a long message write it to a temp file and run `git commit -F <file>`.

### 6. Verify, then repeat

```bash
git log -1 --stat
git status --porcelain
```

If more changes remain, return to step 2 for the next micro commit. Each repetition is its own commit.

## Safety Rules

- Do not change the Git configuration.
- Do not use `--no-verify` unless the user tells you to. Hooks can be in `.git/hooks` or the Git configuration.
- If a hook fails, Git does not make the commit. Fix the problem, stage again, and rerun `git commit`. Do not use `--amend`.
- Do not change commit history unless the user tells you to. No `git reset --hard`, `git rebase`, or `git history`.
- Do not push unless the user tells you to. No force push to the default branch.