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
For process in GPU, use
```bash
nvidia-smi | grep 'python'
```
to find a process with the keyword `'python'`, and to kill, use
```bash
sudo kill -9 ${PID}
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

# TensorBoard
### 1. Launch TensorBoard in SSH remote:
```bash
tensorboard --logdir=/path/to/logs/dir/
```
Not that the DIR_PATH of logfile should be given, NOT the path of the logfile
e.g.
```bash
tensorboard --logdir=/data_hdd/jun/DockerMount/OpenPCDet_docker/output/kitti_models/pv_rcnn_relation_car_class_only/train-CarClass-k16-IP_mlp/20240310-135445/tensorboard/
```
where containing the logfile `events.out.tfevents.1710078885.e8c0683eb2e1`  
then get the return message
```bash
TensorFlow installation not found - running with reduced feature set.

NOTE: Using experimental fast data loading logic. To disable, pass
    "--load_fast=false" and report issues on GitHub. More details:
    https://github.com/tensorflow/tensorboard/issues/4784

I0311 12:00:01.281496 140462065710848 plugin.py:429] Monitor runs begin
Serving TensorBoard on localhost; to expose to the network, use a proxy or pass --bind_all
TensorBoard 2.10.1 at http://localhost:6007/ (Press CTRL+C to quit)
```
Here we get its port in SSH-remote as: `6007`
### 2. Connect local host to remote via this port using SSH command
```bash
ssh -L 6007:localhost:6007 ${username}@${remote_host}
```
launch a web browser in local host, give the page link
```bash
http://localhost:6007
```
Then we get the tensorboard showed in local, which generated in a remote host.
