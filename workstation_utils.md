# Command list
check & edit the file
```bash
vim ${fimename}
```
quit vim
```bash
q
```
run a `.sh` script
```bash
sh ${bash_file.sh}
```

# tmux
```bash
sudo apt install tmux
```
get into tmux without a given name
```bash
tmux
```
### Structure
```bash
Session
|   Window
|   |   Pane
```
### In the same pin Window
- create a new pane horizontally
    `Ctrl` + `B` + `%`
- create a new pane vertically
    `Ctrl` + `B` + `"`
- switch between panes
    `Ctrl` + `B` + `RIGHT/LEFT/UP/DOWN`
- check hardware usage
    ```bash
    htop
    ```
- close the pane
    ```bash
    exit
    ```
### New pin Window
- create a new window
    `Ctrl` + `B` + `C`
    Now we are in the nwely created Window[1]  
    the `*` indicates the WIndow where we are currently  
- switch back to Window [0]
    `Ctrl` + `B` + `0`
- rename current Window
    `Ctrl` + `B` + `,`
    type the name and hit `Enter`

### Sessions
- detach from current session
    `Ctrl` + `B` + `D` from current session
- view the running tmux sessions
    ```bash
    tmux ls
    ```
- get back to the tmux session
    ```bash
    tmux attach -t ${SessionID}
    ```
    all the stuff would be preserved
- rename tmux session OUT IN HOST terminal
    ```bash
    tmux rename-session -t ${SessionID} ${SessionName}
    ```
- create a new session OUT IN HOST terminal
    with a specified name:
    ```bash
    tmux new -s ${SessionName}
    ```
    without given name, the session can be reached through ID by default
    ```bash
    tmux
    ```
- kill sessions that we don't use anymore
    ```bash
    tmux rename-session -t ${SessionID/SessionName}
    ```
- 

# Vim
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