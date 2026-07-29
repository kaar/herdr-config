# herdr-config

Configuration for [herdr](https://herdr.dev).

## Install

```sh
git clone https://github.com/kaar/herdr-config ~/.config/herdr
```

## Scripts

`scripts/` holds the helpers bound in `config.toml`:

| Script      | Binding    | What it does                                                   |
| ----------- | ---------- | -------------------------------------------------------------- |
| `h-open`    | `prefix+f` | Pick a project in `$DEV/` and focus or create its herdr space  |
| `h-what-ai` | `prefix+i` | Show what the agent in the focused pane is doing right now     |
| `h-recap`   | `prefix+shift+i` | Recap of the pane's agent session: summary, files edited, uncommitted work |

Custom commands run through `/bin/sh`, so the bindings reference them as
`$HOME/.config/herdr/scripts/<script>` — no install step or `$PATH` entry needed.

Requirements: `fzf`, `jq`, `$DEV` set (`h-open`), `t-preview` on `$PATH` for the
`h-open` preview pane, and `pi` plus `jq` (`h-what-ai`, `h-recap`).

To run them from a shell too, add `~/.config/herdr/scripts` to `$PATH`.

## Plugins

[herdr plugins](https://herdr.dev/docs/plugins/) are installed from GitHub
with `herdr plugin install`; herdr keeps the installed copies under
`plugins/github/` (gitignored) and records the resolved set in `plugins.json`.

### fzf-url

Fuzzy-find and open URLs visible in the active pane, like
[`wfxr/tmux-fzf-url`](https://github.com/wfxr/tmux-fzf-url). Bound to `prefix+u`
in `config.toml` via the `fzf-url` plugin action; `Enter` opens the selection,
`ctrl-y` copies it, `tab` multi-selects.

```sh
herdr plugin install kaar/herdr-fzf-url
```

See [`kaar/herdr-fzf-url`](https://github.com/kaar/herdr-fzf-url) for options
and details.

## Skills

Agent skills live under `skills/`.

### herdr

Teaches an agent to operate Herdr itself from inside a pane: inspect
workspaces/tabs/panes, split panes and run commands without stealing focus,
read pane output, wait for servers or tests, and start helper agents in
sibling panes. It refuses to act unless `HERDR_ENV=1`, so an agent outside a
Herdr-managed pane can't control a session it doesn't own.

Not part of this repo — install it from its own source:

```sh
npx skills add ogulcancelik/herdr --skill herdr -g
```

### herdr-docs

Reads Herdr's official documentation offline so agents answer Herdr questions
from the docs instead of guessing. It clones the Herdr repo on demand into
`skills/herdr-docs/vendor/herdr/` (git-ignored).

Install it into your agent with the
[`skills`](https://github.com/vercel-labs/skills) CLI:

```sh
# Install the herdr-docs skill from this repo
npx skills add kaar/herdr-config

# List available skills without installing
npx skills add kaar/herdr-config --list
```

See `skills/herdr-docs/SKILL.md` for the full workflow.

## References

- [GitHub](https://github.com/ogulcancelik/herdr)
- [herdr - Docs](https://herdr.dev/docs).
