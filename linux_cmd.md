# Linux cmds
# Give full permission to a folder
```bash
sudo chmod a+rwx ${FolderName}
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
sudo scp -r ${UserName}@${RemoteIP}:${File/FolderPath} ${LocalPath}
```

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
