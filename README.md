# herdr-config

Configuration for [herdr](https://herdr.dev).

## Install

```sh
git clone https://github.com/kaar/herdr-config ~/.config/herdr
```

## Scripts

`scripts/` holds the helpers bound in `config.toml`:

| Script    | Binding    | What it does                                                     |
| --------- | ---------- | ---------------------------------------------------------------- |
| `h-open`  | `prefix+f` | Pick a project in `$DEV/` and focus or create its herdr space    |
| `h-agent` | `prefix+a` | Prompt for a name, open a tab with it, and start `pi` in it      |
| `h-what`  | `prefix+i` | Show what the agent in the focused pane is doing right now       |

Custom commands run through `/bin/sh`, so the bindings reference them as
`$HOME/.config/herdr/scripts/<script>` — no install step or `$PATH` entry needed.

Requirements: `fzf`, `jq`, `$DEV` set (`h-open`), `t-preview` on `$PATH` for the
`h-open` preview pane, `pi` (`h-agent`), and `jq` (`h-what`).

To run them from a shell too, add `~/.config/herdr/scripts` to `$PATH`.

## References

- [GitHub](https://github.com/ogulcancelik/herdr)
- [herdr - Docs](https://herdr.dev/docs).
