# Vim

## 查找

suppose you want to learn more about what `Ctrl-P` does in insert mode. If you merely search for `:h CTRL-P`, you will be directed to normal mode's `Ctrl-P`. This is not the `Ctrl-P` help that you're looking for. In this case, search instead for `:h i_CTRL-P`. The appended `i_` represents the insert mode. Pay attention to which mode it belongs to.

[Learn-Vim/ch00_read_this_first.md](https://github.com/iggredible/Learn-Vim/blob/master/ch00_read_this_first.md)


## replace all occurrences with confirmation 

```vim
:%s/search_pattern/replacement/gc
```

1. `:%s` - This tells Vim to substitute in the entire file (% means "all lines")
2. `search_pattern` - The text you want to find and replace
3. `replacement` - The text you want to replace it with
4. `g` - This flag means "global", i.e., replace all occurrences on each line, not just the first
5. `c` - This flag means "confirm", which will prompt you for confirmation before each replacement