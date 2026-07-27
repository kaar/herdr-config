---
name: herdr-docs
description: Read official Herdr documentation offline. Use when answering questions about Herdr's behavior, configuration, CLI, socket API, keybindings, plugins, agents, agent automation, session state, persistence, marketplace, integrations, or troubleshooting. Clones the docs from source so answers come from the docs instead of guesses.
---

# Herdr Docs

Answer questions about [Herdr](https://herdr.dev) from its official documentation instead of guessing. The docs are open-source Markdown in the main repo and can be read fully offline after a one-time clone.

## Step 1: Ensure the docs are present

Clone or update the docs before reading them:

```bash
scripts/h-docs
```

Run paths relative to this skill directory. The script clones the Herdr repo into `vendor/herdr/` (git-ignored) inside this skill and prints the docs path. Re-run it any time to update to the latest version. It is idempotent: it updates an existing clone with `git pull --ff-only` and otherwise does a shallow clone.

Options:
- `scripts/h-docs --path` prints the docs directory path and exits.
- `scripts/h-docs --full` does a full clone (all history plus version snapshots). Needed only for version-pinned docs (Step 4).

## Step 2: Read the current docs

The live docs source is:

```
vendor/herdr/website/src/content/docs/
```

The URL slug maps directly to the filename, e.g. `https://herdr.dev/docs/socket-api/` -> `socket-api.mdx`.

## Step 3: Pick the right page

| Topic | Page |
|-------|------|
| Overview | `index.mdx` |
| Installation | `install.mdx` |
| Getting started | `quick-start.mdx` |
| Core concepts (workspaces, tabs, panes) | `concepts.mdx` |
| Keybindings | `keyboard.mdx` |
| Working with Herdr | `how-to-work.mdx` |
| Agents | `agents.mdx` |
| Agent automation | `agent-automation.mdx` |
| Session state / lifecycle | `session-state.mdx` |
| Persistence and remote | `persistence-remote.mdx` |
| Configuration guide | `configuration.mdx` |
| Full config reference | `config-reference.mdx` |
| Plugins | `plugins.mdx` |
| Plugin marketplace | `marketplace.mdx` |
| CLI reference | `cli-reference.mdx` |
| Socket API | `socket-api.mdx` |
| Integrations | `integrations.mdx` |
| Agent skill | `agent-skill.mdx` |
| Windows (beta) | `windows-beta.mdx` |
| Troubleshooting | `troubleshooting.mdx` |

Read the specific page that matches the question. Grep the docs directory when the right page is unclear:

```bash
rg -l "search term" vendor/herdr/website/src/content/docs/
```

## Step 4: Version-pinned docs (optional)

For docs matching a specific installed Herdr version, do a full clone (`scripts/h-docs --full`), then read:

```
vendor/herdr/docs/versions/<version>/
```

The version index is `vendor/herdr/docs/versions/manifest.json` (parse with `jq`).

## Step 5: Compact agent references

For a condensed, agent-oriented summary rather than full docs, read:
- `vendor/herdr/website/agent-guide.md`
- `vendor/herdr/SKILL.md`

## Constraints

- Do not rely on `herdr.dev/llms.txt` or per-page `.md` endpoints. They do not exist; the site returns an SPA fallback.
- Read pages from the clone with the read tool. Do not fetch them over the network when the offline clone is available.
