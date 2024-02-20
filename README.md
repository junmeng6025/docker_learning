# Take it easy to work with a remote workstation

# 1. Connect to WS
```bash
ssh {UserName}@{IP_address}
```
then give the password  

### Manage process:
Sometimes an unreleased training process should be killed manually
```bash
ps aux | grep {keyword}
```
here we give `train` as key word to find out the training process.  
Get the Process ID in the list, then kill it by ID:
```bash
kill {ProcessID}
```

# 2. Utils with Linux
Usually there is no more graphical UI available to access files & folders when you work with workstation via your local terminal. All should be execuetd with linux commands. There're some utils that can make your work easier and more efficient:

| func                     | app                       |
| ------------------------ | ------------------------- |
| Multi window; Hanging on session             | [tmux](tmux.md)           |
| Editing                  | [vim](vim.md)           |
| Copy / move files around | [linux_cmd](linux_cmd.md) |
| Dev env                  | [Docker](docker.md)       |
| View hardware usage      | `htop`                    |

# VS-Code Addons
- Remote-SSH
- Dev Containers

# CUDA
## vis nvidia-smi in real time:
```bash
watch -n 0.1 nvidia-smi
```
the nvidia refreshes every 0.1s

## choose GPU device:
in docker, run:
```bash
export CUDA_VISIBLE_DEVICES=1
```
