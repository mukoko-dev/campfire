# AGENTS.md

Rules for every AI coding agent (Claude Code, Cursor, Copilot and the rest)
working in this repository.

The enterprise-wide rules are in
[`nyuchi/.github/AGENTS.md`](https://github.com/nyuchi/.github/blob/main/AGENTS.md)
and the org rules in
[`mukoko-dev/.github/AGENTS.md`](https://github.com/mukoko-dev/.github/blob/main/AGENTS.md).
Both apply here in full. This file adds what is specific to Campfire.

## What this repo is

A fork of [basecamp/once-campfire](https://github.com/basecamp/once-campfire),
a Rails application released by Basecamp under the MIT licence. The fork
carries no Nyuchi-authored application changes: only repository plumbing
(lint configuration, workflow and dependency bumps). Keep it that way unless
the owner asks for a divergence, and say so in the PR when one is made.

## Stack and commands

- Ruby (version in `.ruby-version`), Rails, SQLite, Redis.
- Install: `bundle install`.
- Lint: `bin/rubocop`.
- Security scan: `bin/brakeman`.
- Tests: `bin/rails db:setup test`, and `bin/rails db:setup test:system` for
  the browser tests.
- Run all of the above before opening a PR. CI runs the same commands.

## Branches, releases and merging

- Trunk-based: `main` is the only long-lived branch. There is no `staging`
  branch and no `staging` environment. Work branches off `main` and PRs land
  in `main`.
- PR titles are Conventional Commits: lowercase, imperative subject, no
  trailing period. Put `Closes #n` in the PR description.
- Never disable or weaken a check to get green. Fix the cause or escalate.
- Never commit secrets, `.env` files or credentials. Use the secret store.
- Contribution flow for upstream-style changes is in `CONTRIBUTING.md`.
