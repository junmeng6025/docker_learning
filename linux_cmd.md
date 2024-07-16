# Linux cmds
# Give full permission to a folder
```bash
sudo chmod a+rwx ${FolderName}
```
# Zip files
1) cd to directory containing files to be zipped
  ```bash
  sudo zip -r ../zip_file.zip .
  ```
  > zip file would be generated to the parent path

2) cd to parent path where the folder to be zipped exists
  ```bash
  sudo zip -r /path/to/save/zip_file.zip /path/to/folder
  ```

# Copy and paste
## single file
```bash
cp /path/to/file/to/be/copied /path/to/destination/filename
```
## folder
```bash
cp -r /path/to/folder/to/be/copied /path/to/destination_folder
```
## from SSH Remote to Host
```bash
scp -r ${UserName}@${RemoteIP}:${FolderPath} ${LocalPath}
```
```bash
scp ${UserName}@${RemoteIP}:${Path/To/File} ${LocalPath}
```
```bash
cd ${Expected/Local/Path}
scp ${UserName}@${RemoteIP}:${Path/To/File} .
```
For WSL, use `/mnt` first to direct to local

# Cut and paste (Move file)
```bash
mv /path/to/file/to/be/moved /path/to/destination
```
move to current path:
```bash
mv /path/to/file/to/be/moved .
```
# Delete (Remove)
```bash
rm -rf ${FolderName}
```

# Select GPU device
```bash
export CUDA_VISIBLE_DEVICES=${GPU_id}
```
to check current GPU id:
```bash
echo ${CUDA_VISIBLE_DEVICES}
```

# Visualize DEBUG_LOG
use `rapid-photo-downloader`
```bash
apt-get install rapid-photo-downloader
```
Turn on:
```bash
export QT_DEBUG_PLUGINS=1 
```
Turn off:
```bash
export QT_DEBUG_PLUGINS=0 
```

# Mount folders from another ssh
```bash
sudo sshfs -o allow_other,default_permissions usr_name@ip:/path/to/mount /mount/path/on/host
```
Sometimes the mount maight fail due to connection issues. To redo mount, an `unmount` should be executed first:
```bash
sudo umount -l /mount/path/on/host
```
