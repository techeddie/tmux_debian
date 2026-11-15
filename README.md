# tmux_debian

[tmux](https://github.com/tmux/tmux) config for Debian servers, with plugins included in the repo so it works offline right after cloning.

Part of [dotfiles_debian](https://github.com/techeddie/dotfiles_debian). The installer there sets up tmux and this config.

## Features

- Most actions without prefix via `Alt` key bindings
- Windows and panes start at 1, 50 000 lines of scrollback, no escape delay
- Truecolor support (`Tc` override) for Neovim color schemes
- Mouse off by default, toggle with `prefix m` / `prefix M`
- Minimal status bar: date and time on the right
- Plugins: [tpm](https://github.com/tmux-plugins/tpm), [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect), [tmux-yank](https://github.com/tmux-plugins/tmux-yank), [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum)

## Requirements

tmux 3.2 or newer (Debian 12 ships 3.3a), git.

## Install

Recommended: use [dotfiles_debian](https://github.com/techeddie/dotfiles_debian).

Standalone:

```bash
# tmux from Debian
sudo apt-get update && sudo apt-get install -y tmux git

# Clone and link into ~/.config
mkdir -p ~/opt/dotfiles_debian ~/.config
git clone https://github.com/techeddie/tmux_debian.git ~/opt/dotfiles_debian/tmux_debian
ln -sfn ~/opt/dotfiles_debian/tmux_debian ~/.config/tmux

# Config hardcodes ~/.tmux.conf and ~/.tmux/plugins/tpm, so link both into $HOME
ln -sfn ~/.config/tmux/.tmux.conf ~/.tmux.conf
ln -sfn ~/.config/tmux/.tmux ~/.tmux
```

tpm and tmux-resurrect are part of the repo. Missing plugins from the list are installed with `prefix I` inside tmux.

## Key bindings

Prefix is the default `Ctrl-b`.

**Windows and sessions**

| Key | Action |
|---|---|
| `Alt-n` / `prefix N` / `prefix ,` | new window |
| `Alt-Tab` / `Alt-S` / `Alt-PgDn` | next window |
| `Alt-A` / `Alt-PgUp` | previous window |
| `Alt-W` | window and session tree |
| `Alt-2` / `prefix i` | rename window |
| `Alt-3` | rename session |
| `Alt-D` | detach |
| `Alt-X` | kill session |

**Panes**

| Key | Action |
|---|---|
| `Alt-(` | split side by side |
| `Alt-*` | split top and bottom |
| `Alt-Ctrl-h/j/k/l` or `Alt-Ctrl-arrows` | move between panes |
| `prefix h/j/k/l` | move between panes |
| `Alt-Z` / `Alt-F` | zoom pane |
| `prefix H/J/K/L` | move pane to left / bottom / top / right edge |
| `prefix -` / `prefix 9` | even horizontal layout |
| `prefix +` / `prefix 8` | even vertical layout |
| `prefix =` | tiled layout |
| `Alt-Q` | kill pane |

**Other**

| Key | Action |
|---|---|
| `prefix r` | reload config |
| `prefix m` / `prefix M` | mouse on / off |
| `prefix S` / `prefix R` | save / restore session (resurrect) |
| `prefix I` / `prefix U` | install / update plugins (tpm) |

## Tips

Start fish in tmux regardless of the shell tmux was launched from:

```
# Always start fish in tmux, independent of $SHELL of the calling shell
set -g default-shell /usr/bin/fish
```

Attach to tmux automatically on login (fish, in `~/.config/fish/local.fish`):

```fish
# Attach or create a session, skip inside tmux and lf
if not set -q TMUX; and not set -q LF_LEVEL
    tmux attach 2>/dev/null; or tmux
end
```

## Files

| File | Purpose |
|---|---|
| `.tmux.conf` | config, linked to `~/.tmux.conf` |
| `.tmux/plugins/` | plugins, linked via `~/.tmux` |
