# Agent Guide - jamesrweb

## About this repository

This repository is the GitHub profile repository for James Robb. The profile
README and CV are rendered on the github.com/jamesrweb profile page.

## Layout

```
./
├── .agents/               # agent configuration (DotAgents protocol)
├── .git/                  # git internals
├── node_modules/          # installed dependencies, gitignored
├── .github/
│   └── workflows/         # CI workflow
├── AGENTS.md              # this file
├── CLAUDE.md              # symlink to AGENTS.md
├── CV.md                  # the CV document
├── LICENSE                # proprietary content licence
├── README.md              # the profile README
├── biome.json             # `Biome` configuration
├── package.json           # pnpm manifest and scripts
├── pnpm-lock.yaml         # pnpm lockfile
├── pnpm-workspace.yaml    # pnpm workspace settings
├── .gitattributes         # git attributes
└── .gitignore             # git ignore rules
```

## Commands

| Command       | Purpose                  |
| ------------- | ------------------------ |
| `pnpm format` | Applies formatting fixes |
| `pnpm lint`   | Runs the lint checks     |

Every change must pass `pnpm lint` before it is complete.

## Standards

The rules in this file and in the `.agents/` tree are authoritative for this
repository. Change them deliberately, in those files, rather than working around
them.

## Tooling

Formatting and linting are done via `Biome`. `README.md` is excluded from
formatting because its alert block must keep a fixed shape to render.

## Conventions

The content in `README.md` and `CV.md` describes James Robb professionally, so
content changes require explicit user-provided facts. When editing any bullet
list in `README.md` or `CV.md`, count the entries before and after the edit and
keep the total exact. Never break the CV link in `README.md`.

## CI/CD and releases

CI runs on pushes to `main`, on all pull requests, and on manual dispatch. There
is no CD and nothing is published.

## Guardrails

Never fabricate professional content. Never disable or skip a lint or format
gate to make a change pass. Fix the code, not the gate.

## Pointers

- `.agents/agents.md` - the slim agent guidelines for this repository
- `.agents/knowledge/repo-overview/` - the injected repo overview note
- `README.md` - the human-facing documentation

## Open topics

- None.
