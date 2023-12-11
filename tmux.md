# tmux
```bash
sudo apt install tmux
```
get into tmux without a given name
```bash
tmux
```
## Structure
```bash
Session
|   Window
|   |   Pane
```
## Manipulate tmux windows
1. Hit [ <kbd>Ctrl</kbd> + <kbd>B</kbd>] to wait for short-cut keys
2. Then, press the short-cut keys to do what you want

    ### Pane
    |               Hot key               | Function                                       |
    | :---------------------------------: | ---------------------------------------------- |
    |                 `%`                 | create a new pane horizontally                 |
    |                 `"`                 | create a new pane vertically                   |
    | `RIGHT`<br>`LEFT`<br>`UP`<br>`DOWN` | switch between panes                           |
    |                 `o`                 | switch pane                                    |
    |                 `x`                 | close the pane                                 |
    |                 `!`                 | kill all other panes,<br>keep the current only |
    |                 `q`                 | show the number of panes                       |
    ### Window pin
    | Hot key | Function            |
    | :-----: | ------------------- |
    |   `c`   | create a new window |
    |   `,`   | rename the window   |
    |   `w`   | show the window     |
    |  `NUM`  | select the window   |
    |   `p`   | to the *previous*   |
    |   `n`   | to the *next*       |
    ### Session
    | Hot key             | Function                                    |
    | :------------------ | ------------------------------------------- |
    | `:new Session name` | create a new session<br>with the given name |
    | `$`                 | rename current session                      |
    | `s`                 | switch session                              |
    | `d`                 | detach session<br>(minimize, not kill)      |
    | `Ctrl+z`            | hang on the session, return to bash         |

    ***
### commands
- activate mouse 
  ```bash
  tmux set -g mouse on
  ```
- view the running tmux sessions
    ```bash
    tmux ls
    ```
- get back to the tmux session
    ```bash
    tmux attach -t ${SessionID}
    ```
    all the stuff would be preserved  
    to QUIT but NOT KILL the session:  
    Ctrl + B: Ctrl + Z
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
    tmux kill ${SessionID/SessionName}
    ```
