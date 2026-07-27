# AGENTS.md

Guidance for AI agents working in this repository.

## Herdr documentation (read this before answering Herdr questions)

This repo configures [Herdr](https://herdr.dev). When a task involves Herdr's
behavior, config, CLI, socket API, keybindings, plugins, or agents, consult the
official docs instead of guessing. They are open source and can be read fully
offline.

### Where to read the docs

1. Run `./scripts/h-docs` once to clone the Herdr repo locally. It lands in
   `vendor/herdr/` (git-ignored) by default. Re-run it any time to update.
2. Read the Markdown source under:

   ```
   vendor/herdr/website/src/content/docs/
   ```

   The URL slug maps directly to the filename, e.g.
   `https://herdr.dev/docs/socket-api/` -> `socket-api.mdx`.

   Key pages: `index.mdx`, `install.mdx`, `quick-start.mdx`, `concepts.mdx`,
   `keyboard.mdx`, `how-to-work.mdx`, `agents.mdx`, `agent-automation.mdx`,
   `session-state.mdx`, `persistence-remote.mdx`, `configuration.mdx`,
   `config-reference.mdx`, `plugins.mdx`, `marketplace.mdx`,
   `cli-reference.mdx`, `socket-api.mdx`, `integrations.mdx`,
   `agent-skill.mdx`, `windows-beta.mdx`, `troubleshooting.mdx`.

3. Historical, version-pinned docs (for the exact Herdr version installed) live
   under `vendor/herdr/docs/versions/<version>/` (needs a full clone:
   `./scripts/h-docs --full`). The version index is
   `vendor/herdr/docs/versions/manifest.json`.

4. `vendor/herdr/website/agent-guide.md` and root `vendor/herdr/SKILL.md` are
   compact agent-oriented references.

- `./scripts/h-docs --path` prints the docs directory path.
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
