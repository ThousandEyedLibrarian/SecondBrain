### Vertical Movement

| Combo       | Effect                                           |
| ----------- | ------------------------------------------------ |
| # + j/k     | Up or down by relative line number               |
| Ctrl + u/d  | Up or down by half a page                        |
| Shift + [ ] | Up or down page by blocks of text                |
| Ctrl + i/o  | Up or down the jump list (recent jump locations) |
| o           | Insert above current line for editing            |
| Shift + o   | Insert below current line for editing            |
| %           | Jump between braces                              |
### Horizontal Movement

| Combo       | Effect                                                         |
| ----------- | -------------------------------------------------------------- |
| W/B         | Jump along line by next/prev word                              |
| w/b         | Jump along line by next/prev symbol or word                    |
| f + char    | Jump along line by said char (Move to prev/next using ; and ,) |
| Shift + a/i | Jump to front or end of line in insert mode                    |

### Pattern Jumping

| Combo    | Effect                                                |
| -------- | ----------------------------------------------------- |
| vi + sym | Highlight everything in between symbols excl. symbols |
| va + sym | Highlight everything between symbols incl. symbols    |
| ya + sym | Yank everything between symbols incl. symbols         |
| *        | Enter word under cursor as search                     |
| * + n/N  | Enter word under cursor as search and jump instances  |

### Editing

| Combo         | Effect                                                |
| ------------- | ----------------------------------------------------- |
| cmd + iw      | Execute some motion from anywhere in a word (e.g diw) |
| m + num/char  | Set bookmark at location                              |
| \` + num/char | Jump to bookmark                                      |
| gv            | Highlight last selection                              |

See also:
- [[Vim and Neovim]]
- [Vim Motions Strategy Guide - Jonkero](https://www.youtube.com/watch?v=ibNvyTD4Icg)
- [Vim Motions Strategy Guide Part 2 - Jonkero](https://www.youtube.com/watch?v=zGijq0rUsig)
