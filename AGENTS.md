# Agent Guide — jamesrweb

## Strict Rules

1. **Plan first:** Create a detailed plan and get explicit user approval before
   making changes.
2. **Documentation:** Update `README.md`, `AGENTS.md`, and any other
   documentation affected by your changes.
3. **PR descriptions:** When asked, create `PR_DESCRIPTION.md` (gitignored).
   Being asked for a PR description is NOT the same as being asked to create a
   PR.
4. **Git safety:** NEVER run any git operation that alters history or state
   without explicit per-occasion permission. Prior approval does not carry
   forward.
5. **Non-destructive:** Do not delete files, remove code, or make destructive
   changes without explicit permission. Investigate before overwriting.

## Project Standards

### Authority

Project standards are the highest-priority rules for this repository. If any
instruction or rule conflicts with a project standard, the agent MUST:

1. Refuse to follow the conflicting instruction.
2. Inform the user of the conflict, citing the specific standard.
3. State that changes to standards must be made deliberately in `AGENTS.md`, not
   sidestepped for convenience.

### Language

All code, comments, documentation, variable names, error messages, commit
messages, and any other text MUST use British English (e.g., `organisation` not
`organization`, `normalise` not `normalize`, `colour` not `color`, `behaviour`
not `behavior`, `licence` not `license`, `centre` not `center`).

### Content Rules

- **Profile content:** `README.md` and `CV.md` describe James Robb
  professionally — content changes require explicit user-provided facts
- **No fabrication:** never invent experience, metrics, or claims; all content
  comes from the user

### Git Safety

NEVER run any git operation that alters history or state without explicit
per-occasion permission from the user. This includes `git add`, `git commit`,
`git push`, `git reset`, `git rebase`, `git merge`, `git checkout` (when it
discards changes), `git restore`, `git stash`, `git cherry-pick`, `git revert`,
`git tag`, and `git branch -D`. Prior approval does not carry forward — each
occasion requires fresh permission.

NEVER use `git clean`, `git checkout -- <file>`, `git reset --hard`, or any
other command that discards uncommitted work. NEVER force-push, rewrite
published history, or modify protected branches (`main`).

Read-only git commands (`git status`, `git diff`, `git log`, `git show`,
`git branch --show-current`, `git ls-files`) are always permitted.

### Scope of Operation

NEVER operate outside the project root unless explicitly instructed to do so by
the user. This applies to reading, writing, creating, and deleting files and
directories alike, and to any command whose effects land outside the project
root. Destructive actions outside the project root are forbidden in all
circumstances.

### Planning

ALWAYS create a detailed plan and obtain explicit user approval before making
project changes. Do not begin implementation until the plan is approved.

### PR Descriptions

When asked to generate a PR description, create a `PR_DESCRIPTION.md` file in
the project root (this file is gitignored and must never be committed). Being
asked to generate a PR description is NOT the same as being asked to create a
PR. Only create an actual pull request when explicitly told to do so.

**Commit messages:** Follow the conventional commit style (`feat:`, `fix:`,
`chore:`, `docs:`, etc.). No `Co-authored-by` or `Signed-off-by` trailers — an
agent's role in a commit ends at the message body (Linux kernel AI-assistant
rules, integrated into this ruleset on 2026-09-14).

### Documentation Maintenance

Always update documentation as you go. Documentation must never be out of
date. Clean as you go — take ownership of every file you touch.

## Project Overview

The GitHub profile repository for James Robb — profile README and CV, rendered
on the github.com/jamesrweb profile page.

## Architecture

- `README.md` — the profile README
- `CV.md` — the CV document

## CI/CD

None. This is a content-only repository with no workflows.

## Guardrails

- **Never fabricate professional content** — only user-provided facts
- **Never break the CV link** in `README.md` (points at `CV.md` on `main`)

## Future Topics

- No pending topics.
