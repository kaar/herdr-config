# fzf-url

Fuzzy-find and open URLs visible in the active [herdr](https://herdr.dev) pane, like [`wfxr/tmux-fzf-url`](https://github.com/wfxr/tmux-fzf-url).

It reads the active pane's recent scrollback, extracts `http(s)://` and `www.` URLs, dedupes them (most recent on top), and shows them in an fzf popup.

## Install

```sh
herdr plugin install kaar/herdr-config/plugins/fzf-url
```

Then bind the action in `~/.config/herdr/config.toml`:

```toml
[[keys.command]]
key = "prefix+u"
type = "plugin_action"
command = "fzf-url"
description = "fzf open URL from pane"
```

Reload the config:

```sh
herdr server reload-config
```

## Use

Press your bound key (`prefix+u`) in any pane. The action id `fzf-url` is
globally unique, so the unqualified id works; use `kaar.fzf-url.fzf-url` if it
ever collides with another plugin.


| Key      | Action                                |
| -------- | ------------------------------------- |
| `Enter`  | Open the selected URL(s)              |
| `ctrl-y` | Copy the selected URL(s) to clipboard |
| `tab`    | Multi-select several URLs             |

## Requirements

- herdr `>= 0.7.4`
- `fzf`
- macOS (`open`, `pbcopy`) or Linux (`xdg-open`, and `wl-copy` / `xclip` / `xsel`)
- `jq` only when the source pane id cannot be resolved from the environment

## Configuration

| Environment variable | Purpose                                          |
| -------------------- | ------------------------------------------------ |
| `H_URL_LINES`        | Scrollback lines to scan (default: `2000`)       |
| `H_URL_OPENER`       | Override the opener, e.g. `open -a Firefox`      |

## How it works

Herdr plugin actions run without a TTY, so the `fzf-url` action opens a
session-modal popup pane and forwards the active pane id through
`SOURCE_PANE_ID`. The popup runs the picker, which captures the pane with
`herdr pane read --source recent-unwrapped`, extracts URLs, and runs fzf.

## Local development

```sh
herdr plugin link ~/.config/herdr/plugins/fzf-url
herdr plugin action list --plugin kaar.fzf-url
herdr plugin action invoke fzf-url
```
