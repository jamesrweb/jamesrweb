---
kind: note
id: repo-overview
title: Repo overview - jamesrweb
context: auto
summary: What the profile repository is, how it is laid out, and how CI lints it.
tags: overview, architecture, profile
---

# Repo overview - jamesrweb

## What this is

The GitHub profile repository for James Robb. The profile README and the CV
document are rendered on the github.com/jamesrweb profile page. Content is
proprietary.

## Architecture

- `README.md` - the profile README
- `CV.md` - the CV document, linked from `README.md`
- `biome.json`, `package.json`, `pnpm-workspace.yaml`, `pnpm-lock.yaml` - the
  `Biome` and pnpm tooling configuration

## Commands

| Command        | Purpose              |
| -------------- | -------------------- |
| `pnpm format`  | Apply `Biome` fixes  |
| `pnpm lint`    | `Biome` check        |
| `pnpm install` | Install dependencies |

## CI/CD

CI (`continuous-integration.yml`) runs on pushes to `main`, on all pull
requests, and on manual dispatch. Its job is `lint`, run after
`pnpm install --frozen-lockfile`. Concurrency cancels in-progress runs. There is
no CD workflow.

## Formatting note

`README.md` is excluded from `Biome` formatting via an override in `biome.json`.
Its GitHub alert block requires the marker to stand alone on its opening line,
which a Markdown formatter collapses, so the alert would stop rendering. Remove
the override from `biome.json` when the alert block is removed from `README.md`.
