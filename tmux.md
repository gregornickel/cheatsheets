# tmux

Small tmux wiki

## Sessions

Start using tmux by creating a session. Multiple sessions can be created and you can attach and detach from sessions. Sessions continue to run in the background if you detach.

- Start session `tmux`
- List all sessions `tmux ls`
- Start session with session name `tmux new -s session_name`
- Attach to session `tmux attach -t session_name`
- Kill a session `tmux kill-session -t0`
- Kill all sessions `tmux kill-server`

## Shortcuts

While attached to a session you need to run the default **prefix** `ctrl + b` to run a tmux command. For the shortcut `c` you need to type `<ctrl + b> + c`.

Note: I changed the default prefix to `ctrl + j`

- Show all available shortcuts `<prefix> + ?`
- Detach from a session `<prefix> + d`
- Change session numbering `<prefix> + $`

### Windows

The current session is displayed at the bottom in the bar with squared brackets. Followed by the windows of the session displayed with number and name, e.g. `0:zsh`.

- Create a window `<prefix> + c`
- Change window name `<prefix> + ,`
- Kill the current window `<prefix> + &`

Switch between windows:

- Switch to last window `<prefix> + l`
- Switch to previous window `<prefix> + p`
- Switch to next window `<prefix> + n`

### Panes

You can split a window into several panes. 

- Split pane horizontally `<prefix> + "`
- Split pane vertically `<prefix> + %`
- Kill current pane `<prefix> + x`

Switch between panes:

- Switch panes with arrow keys `<prefix> + ↓`
- Switch between layouts `<prefix> + space`

## Configuration File

tmux can be easily customized with a `.tmux.conf` configuration file. Create the file in your home directory:

```shell
vim ~/.tmux.conf
```

My `.tmux.conf` file:

```
# correct import of the shell .rc file
set -g default-command "$SHELL"

# remap prefix from 'C-j' to 'C-j'
unbind C-b
set-option -g prefix C-j
bind-key C-j send-prefix

# enable mouse mode (a.o. adjust split pane sizes)
set -g mouse on
```

