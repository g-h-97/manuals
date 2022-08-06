

# Split horizontally & vertically

Press `ctrl+b`, then release them, then press `"`
Press `ctrl+b`, then release them, then press `%`

# Synchronise all windows

Press `ctrl+b`, then type `:setw synchronize-panes`, then press `Enter`
You can also bind it to a key, in `.tmux.conf` or `.config/tmux/tmux.conf` as follows:

```
# toggle synchronize-panes
bind C-x setw synchronize-panes
```

The sync status can be shown by adding the following lines:

```
setw -g window-status-current-format '#{?pane_synchronized,#[bg=red],}#I:#W'
setw -g window-status-format         '#{?pane_synchronized,#[bg=red],}#I:#W'
```
