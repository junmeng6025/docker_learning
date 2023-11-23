# vim
## some times without `sudo` we just have read-only permission
create a new file via vim
```bash
vim ${filename.suffix}
```
`:q`: quit vim  
`:q!`: quit, discard all changes  
`:wq`: save and quit  
### Modes:
`i`: insert  
`:`: cmd  
`v`: visual  
### Move the cursor
`h`: <  
`j`: v  
`k`: ^  
`l`: >  

`x`: delete  
`dd`: quickly delete the whole line  
`u`: undo  
### Edit the text
`:set number`: show line numbers  
`:2`: navigate to line 2  
`i`: get into insert mode, then use `j` and `k` to navi  
`Esc`: quit insert mode  

`+p`: paste text from clip board  
`:w`: save the changes  
`:!`: run command  