# h-nav

Vim-aware `ctrl+h/j/k/l` directional pane focus for [herdr](https://herdr.dev) — the herdr half of the [vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator) pattern.

When the focused pane's foreground process is vim-like (vi/vim/nvim/gvim/view/lvim/… or fzf), the chord is passed through to it; nvim's own mapping (see `nvim-config/nvim/plugin/herdr_navigator.lua`) hands navigation back to herdr when a window move hits its layout edge. Otherwise focus moves to the neighbouring herdr pane directly.

## Install

```sh
herdr plugin install kaar/herdr-config/plugins/h-nav
```

Then bind the actions in `~/.config/herdr/config.toml`, using the qualified
action ids (the local ids `left`/`down`/`up`/`right` are too generic to be
globally unique):

```toml
[[keys.command]]
key = "ctrl+h"
type = "plugin_action"
command = "kaar.h-nav.left"
description = "focus pane left (vim-aware)"

[[keys.command]]
key = "ctrl+j"
type = "plugin_action"
command = "kaar.h-nav.down"
description = "focus pane down (vim-aware)"

[[keys.command]]
key = "ctrl+k"
type = "plugin_action"
command = "kaar.h-nav.up"
description = "focus pane up (vim-aware)"

[[keys.command]]
key = "ctrl+l"
type = "plugin_action"
command = "kaar.h-nav.right"
description = "focus pane right (vim-aware)"
```

Since the direct chords are taken by navigation, restore clear-screen on a
prefixed chord (vim-tmux-navigator's `prefix C-l` equivalent):

```toml
[[keys.command]]
key = "prefix+ctrl+l"
type = "shell"
command = "\"$HERDR_BIN_PATH\" pane send-keys \"$HERDR_ACTIVE_PANE_ID\" ctrl+l"
description = "send ctrl+l (clear screen) to pane"
```

Reload the config:

```sh
herdr server reload-config
```

## Use

| Focused pane      | `ctrl+h/j/k/l` does                                   |
| ----------------- | ----------------------------------------------------- |
| shell / other     | moves herdr pane focus left/down/up/right              |
| vim / nvim        | moves vim windows; crosses out to herdr at the edge    |
| fzf               | `ctrl+j/k` move the selection (chord passed through)   |

## Requirements

- herdr `>= 0.7.4`
- macOS or Linux

## How it works

Each action runs `h-nav <direction>` with the plugin directory as cwd. The
script asks `herdr pane process-info` for the focused pane's foreground
process; if the name matches the vim/fzf pattern it forwards the chord with
`herdr pane send-keys`, otherwise it calls `herdr pane focus --direction`.
The pane id comes from `HERDR_PANE_ID` (plugin actions) with a fallback to
`HERDR_ACTIVE_PANE_ID`, so the same script also works as a bare
`type = "shell"` keybinding.

## Local development

```sh
herdr plugin link ~/.config/herdr/plugins/h-nav
herdr plugin action list --plugin kaar.h-nav
herdr plugin action invoke kaar.h-nav.left
herdr plugin log list --plugin kaar.h-nav
```
