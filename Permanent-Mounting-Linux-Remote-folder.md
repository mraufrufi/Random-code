# Create an NFS server on Oracle Linux

Open a terminal and connect to your server instance.

Install the NFS utilities package.

``` sudo yum install -y nfs-utils```
## Create an NFS Share
Create a directory to contain your shared files.

``` sudo mkdir /nfs-share ``

Create a series of test files.
```
sudo fallocate -l 10MB /nfs-share/file1
sudo fallocate -l 10MB /nfs-share/file2
echo "This is a shared text file." | sudo tee /nfs-share/shared-text.txt > /dev/null
```

Verify the files created successfully.
```
ls -lh /nfs-share
```
Change permissions on the files.

```
sudo chmod -R 777 /nfs-share
```
Define the share in /etc/exports.
Each entry has the format export host1(options1) host2(options2) host3(options3).
```
echo "/nfs-share  <CLIENT_IP_ADDRESS>(rw)" | sudo tee -a /etc/exports > /dev/null
```
### Start the NFS Server
add nfs into firewall
```
sudo firewall-cmd --permanent --zone=public --add-service=nfs
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```
Enable and start the NFS service.
```
sudo systemctl enable --now nfs-server
showmount -e
```

## Install the NFS Utilities Package on the Client 
```
sudo dnf install -y nfs-utils
```
Create a directory for the mount point.
```
sudo mkdir /nfs-mount
```
Mount the share and get a directory listing.
```
sudo mount <SERVER_IP_ADDRESS>:/nfs-share /nfs-mount
ls -lh /nfs-mount
```
