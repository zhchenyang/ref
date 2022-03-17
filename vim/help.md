# vim

`C-r` redo 

`iskeyword`, is part of a word? keywords are used in searching and recongnizing with `w`, `*`, `[i` etc. 

`[i`: Display the first line that contains the keyword under the cursor. 
`]i`: like above, but start at the current cursor position.
`N%`: Go to \{conut\} percentage in the file, on the first non-blank in the line _linewise_.
`H/M/L`: TO line Home/Middle/low
`C-g`: prints the current file name, the cursor position, and file status.
`ruler`: show the line and column number of the cursor position, separated by a comma.
`C-U/E/F`: up
`C-D/Y/B`: down 

## general

`:set autosave`

## searching

`:set noignorecase`: Not ignore case
`:set hlsearch`: high light searching
`:set nohlsearch`: not high light searching
`:set incsearch`: high light searching while typing
`:set nowrapscan`: stop search end of the file.

if you don't want to turn `hlsearch` on, but want to highlight all matches while searching, you can turn off it with autocmd. Example:

```vimscript
augroup vimrc-incsearch-highlight
  autocmd!
  autocmd CmdlineEnter /.\? :set hlsearch
  autocmd CmdlineLeave /.\? :set nohlsearch
augroup END
```

## moving

`\``: jump to marks

special marks

`'` where come from
`"` last edit
`[` last edited start
`]` last edited end

## help

check error code

`:help E63`

## edit

`[w]next`: save and next
`next!`: discard and next
`previous`

just view file `view file.name`

## windows

`[v|h]split [file\_name]`, `[v|h]new`

resize `C-w +/-`
movement `C-w + h/j/k/l/t/b`
swap windows `C-w H/J/K/L`
quit all `qall`
save all `wall`

TODO `tab`
