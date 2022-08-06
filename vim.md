# All Possible Keys


```
h               move left a char
j               move down a line
k               move up a line
l               move right a char
/               search

f[c]            find next occurance of a character
F[c]            find previous occurance of a character
t[c]            til the next occurance of a character exclusive
T[c]            til the previous occurance of a character exclusive

ct[c]           change til the next char exclusive
cT[c]           change til the previous char exclusive
cf[c]           change find the next char inclusive
cF[c]           change back find the previous char inclusive

dt[c]           delete til the next char exclusive
dT[c]           delete til the previous char exclusive
df[c]           delete find the next char inclusive
dF[c]           delete back find the previous char inclusive
```

# Scroll Bind

In order to scroll two windows in the same time use `:set scb!` or `:set scrollbind` on each one, then run `:syncbind` in order to the scrolling to follow the number of lines you are scrolling.

# Vim Symbolic Links

To create a symbolic link that can be opened in vim without causing it to be empty, the must be create using absolute paths in the `ln` command. Here is an example of a working and none working scenarios

## Working

```
ln -s /home/user/file /home/user/.config/file_sym_link

# Equivalently
ln -s ~/file ~/.config/file_sym_link
```

Now when you vim the `file_sym_link` file it should appear correctly.

## None Working

```
cd /home/user
ln -s file .config/file_sym_link
```

In this case opening the file `.config/file_sym_link` will open the file, however it will be completely empty as if you've created a new file with that name, which is obviously not what we want.
