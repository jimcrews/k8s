### ~/.vimrc

```
set ts=2 sts=2 sw=2
set ts=2 sts=2 sw=2
set expandtab
set number ruler
set autoindent smartindent
syntax enable
filetype plugin indent on

set belloff=all
```

### Indent a code block using spaces:
  1. enter visual block mode using `ctrl + v`
  2. select block
  3. go into special insert using `shift + i`
  4. press `esc` to see changes

### Delete Block
  1. enter Visual Block `shift + v`
  2. select block
  3. press `d` to delete


### misc

 - Show potential tabs: `:set list`, `:set nolist`
 - Replace tabs with spaces: `:retab`

 - Set Cursor Column: `set cursorcolumn`, `set nocursorcolumn`
 - Undo: `:u`
 - To turn off autoindent when you paste code: `:set paste`
 - Turn off paste-mode (auto-indenting works again): `:set nopaste`
 - Turn off the annoying bell: `:set belloff=all`
 - Enable syntax highlighting: `:syntax on`