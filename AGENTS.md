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
- **Bullet completeness:** when editing any bullet list in `README.md` or
  `CV.md`, count the entries before and after the edit. Every pre-existing
  bullet must survive unless the user explicitly approved its removal or merge,
  and the post-edit count must match the expected total exactly

### Formatting

- **Prettier** formats the repository's Markdown (`CV.md`, `AGENTS.md`) with
  `--prose-wrap always`, producing an 80-column prose wrap and realigned
  tables covering the whole repository, for example
  `prettier --write --prose-wrap always .`
- **`README.md` is excluded from Prettier formatting**: its GitHub alert
  block requires `> [!IMPORTANT]` to stand alone on the opening line, which
  Prettier's prose wrapping collapses, so the alert would stop rendering;
  its prose is wrapped manually to the same 80-column style instead
- **Prettier output is accepted as the source of truth as run** — no
  content-drift verification is required after formatting
- `CLAUDE.md` is a symlink to `AGENTS.md` and needs no separate handling
- `LICENSE` has no Prettier parser and is left untouched
- Format-only changes are committed as `style:` commits
  (for example `style: Format the repository files with Prettier`)

### Git Guardrails

**Permission rule:** never run any git command that alters history, state, or
the working tree without the user granting explicit per-occasion permission,
whether run directly or through a wrapper such as the `gc` helper. Prior
approval does not carry forward, and authorisation for one operation never
authorises another. Read-only inspection is always allowed.

**Always allowed (read-only):** `git status`, `git diff`, `git log`, `git show`,
`git branch --show-current`, `git ls-files`, `git stash list`, and `git fetch` /
`git pull` (the user classifies both as effectively read-only).

**Branch rule:** agents stay on the branch the session started on. Never
`git switch`, `git checkout <branch>`, or create branches (`git branch`,
`git switch -c`) unless the user names the branch or explicitly asks to work on
one. Prefer modern verbs (`switch`, `restore`, `revert`) over `checkout` in
general, matching the user's practice.

**Prohibited without per-occasion permission:**

- Staging and committing: `git add`, `git commit` (including `--amend`), the
  `gc` helper
- Publishing: `git push` (any mode)
- History rewriting: `git rebase`, `git merge`, `git cherry-pick`, `git revert`,
  commits with `--amend`
- Moving HEAD or the index: `git reset` in any mode (`--soft`, `--mixed`,
  `--hard`)
- Discarding working-tree changes: `git restore`, `git checkout -- <path>`
- Stash mutation: `git stash` (create, pop, apply, drop)
- Ref and branch creation/deletion: `git tag`, `git branch -d/-D`,
  `git worktree add`
- Plumbing bypasses: `--no-verify`, editing `.git/` internals, `git config`
  changes, disabling hooks

**Absolute prohibitions, regardless of any prior approval:** force-pushing
(`--force`, `--force-with-lease`) on any branch; rewriting already-published
commits on `main`; deleting branches others may depend on; and running any
command that discards uncommitted changes unless the user names those changes as
expendable in the same instruction.

**Precedence:** without fresh, explicit permission covering the exact operation,
no instruction overrides these rules; name the command, ask, and wait.

### Scope of Operation

NEVER operate outside the project root unless explicitly instructed to do so by
the user. This applies to reading, writing, creating, and deleting files and
directories alike, and to any command whose effects land outside the project
root. Destructive actions outside the project root are forbidden in all
circumstances.

**The one exception:** Experiments and scratch work belong in the `/tmp`
directory — and only when the user has asked for them or given permission.
Anything created there is still subject to the same non-destructive rules: do
not delete, overwrite, or modify anything in `/tmp` that the agent did not
create itself.

### Obligation to Fix

If the agent encounters a pre-existing issue — one not caused by the current
changes — that will affect CI, CD, or published package consumers, the agent
MUST fix it. This is NOT optional. The agent must not ignore, skip, or defer
such issues regardless of whether they were introduced by the agent's own
changes. A broken pipeline or a broken published package is the agent's
responsibility if the agent is aware of it.

### Planning

ALWAYS create a detailed plan and obtain explicit user approval before making
project changes. Do not begin implementation until the plan is approved.

### PR Descriptions

When asked to generate a PR description, create a `PR_DESCRIPTION.md` file in
the project root (this file is gitignored and must never be committed).

**Important:** Being asked to generate a PR description is NOT the same as being
asked to create a PR. Only create an actual pull request when explicitly told to
do so.

**Commit messages:** Commit with the user's `gc` helper per the Git Guardrails
section — `source ~/.bash_aliases && gc -m "<subject>" [-m "<description>"]`. It
stages everything and appends the user's `Signed-off-by` trailer automatically;
it suits the final commit of a batch, and for split commits, stage and commit
earlier pieces manually with `git commit --signoff` (identical trailer).
Conventional-commit subjects (`feat:`, `fix:`, `chore:`, `ci:`, etc.), British
English, no emoji prefixes for human-authored commits — they only appear on
automated Dependabot commits where such automation exists.

**No co-authored commits:** Agents MUST NOT add `Co-authored-by` trailers or any
other attribution that signs off a commit on the agent's behalf. Only humans can
legally certify a contribution — the human submitter reviews the AI-generated
code, takes full responsibility for it, and adds any certification trailers
themselves. Following the rules the Linux kernel team enforce for AI coding
assistants, an agent's role in a commit ends at the message body — no
`Signed-off-by` appended by the agent, no `Co-authored-by`, no other trailers or
sign-offs authored on the agent's behalf. The user's own sign-off appended
automatically by the `gc` helper differs; it certifies the user's content on the
user's explicit instruction and is unaffected by this rule. This distinction was
integrated into this ruleset on 2026-10-12. See [AI Coding Assistants — The
Linux Kernel documentation]
(https://docs.kernel.org/process/coding-assistants.html), integrated into this
ruleset on 2026-09-14.

**Assisted-by attribution:** Where attribution for AI assistance is wanted, use
an `Assisted-by: LLM` trailer in the commit message body rather than a co-author
or sign-off trailer. It records that the contribution was produced with AI
assistance without certifying or authoring it. This mirrors the kernel's
`Assisted-by: LLM [TOOL1] [TOOL2]` format — optionally list specialised analysis
tools after `LLM`, but never list basic development tools (git, compilers,
editors, linters). Only add the trailer when the user has asked for AI
attribution; the default is no trailer at all.

### Documentation Maintenance

Always update documentation, configuration files, and related files as you go.
Documentation must never be out of date. If a change affects `README.md`,
`AGENTS.md`, configuration files, or any other documentation, update them in the
same change. Clean as you go — take ownership of every file you touch.

If formatting, linting, or other tooling fixes issues in files you did not
originally author, do not revert those fixes. CI would break again. Accept
responsibility for the state of the codebase after your changes, not just the
lines you intended to change.

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
