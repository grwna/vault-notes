# Core
https://vim.rtorr.com
# LazyVim
https://cheatography.com/thesujit/cheat-sheets/lazyvim-neovim/
[[LazyVim for Ambitious Devs|Tutorial]]
# Motions
## Normal Mode
### Basic
`r` - replace
`d` - delete
	
### Rack your brains
`gi`- Enter insert mode at the last place before exiting insert mode
`I`, `A` - insert mode to first or end of line
`$, ^` - go to last column of line and to first non indent character
`CTRL + {f/b,d/u,e/y}` - Scrolling pages 
`zz, zb, zt` - Scrolling pages easily
`f, F` - find mode (like seek mode)
`t`, `T` - Til mode, like find, but to just before

>[!important]
>Modification commands like `d` work as well with `f` or `t` to delete to a certain character

`w,e,b` words and `ge` - moving by words. **Also have Shift versions**
`{count}G` - go to a line number

`gd` - go to definition
`gf` - go to file (imports)
`%` - jump to matching brackets `({[]})`
## Command Mode
`:e {filepath}` - open path from anywhere 