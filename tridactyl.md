# Fix Search

These key binding are going to make the search in tridactyl works just like in Vim, instead of the firefox default way `Ctrl+G` & `Ctrl+Shift+G`

```
bind / fillcmdline find
bind ? fillcmdline find -?
bind n findnext 1
bind N findnext -1
bind ,<Space> nohlsearch
```
