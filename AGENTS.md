# AGENTS.md

Guidance for AI agents working in this repository.

## Herdr documentation (read this before answering Herdr questions)

This repo configures [Herdr](https://herdr.dev). When a task involves Herdr's
behavior, config, CLI, socket API, keybindings, plugins, or agents, consult the
official docs instead of guessing. They are open source and can be read fully
offline.

Use the `herdr-docs` skill in this repo. Read `skills/herdr-docs/SKILL.md` and
follow it: it clones the Herdr repo on demand and points you at the right doc
page.

- Skill: `skills/herdr-docs/SKILL.md`
- Clone/update the docs: `skills/herdr-docs/scripts/h-docs` (lands in
  `skills/herdr-docs/vendor/herdr/`, git-ignored; re-run any time to update).
- Docs source after cloning:
  `skills/herdr-docs/vendor/herdr/website/src/content/docs/`.
- Background and rationale: `docs/research/herdr-offline-docs.md`.

Do not rely on `herdr.dev/llms.txt` or per-page `.md` endpoints; they do not
exist (the site returns an SPA fallback for them).

## Tool usage

- Never use `sed` or `cat` to read files; use the read tool.
- Use `rg` (ripgrep) instead of `grep`.
- Use `jq` for parsing JSON/JSONL.

## Editing

- Read files in full before editing. Keep edits minimal.

## Git

- Only stage files you changed: `git add <specific-files>`.
- Never use `git add -A`, `git add .`, `git reset --hard`, `git stash`, or
  `git commit --no-verify`.
- Run `git status` before committing.

## Style

- Be concise and direct. No emojis in commits, issues, PRs, or code.
- Avoid em dashes as sentence interrupters.
