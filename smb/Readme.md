## Mount a smb share in linux

create a mountpoint

```sh
mkdir /mnt/smb
```

Install libraries to support smb share

```sh
sudo apt install cifs-utils
```

create a credentials-file
```sh
sudo cat > /etc/win-credentials <<EOF
username=user
password=password
domain=domain
EOF
```

change the permissions

```sh 
chmod 600 /etc/win-credentials
chown root:root /etc/win-credentials
```

mount the share 

```sh
mount -t cifs -o credentials=/etc/win-credentials //WIN_SHARE_IP/<share_name> /mnt/smb
```
## Automount smb share during startup

create a entry in the fstab fiel

```sh
sudo sh -c 'echo "//WIN_SHARE_IP/<share_name>  /mnt/smb  cifs  credentials=/etc/win-credentials,file_mode=0755,dir_mode=0755 0       0" >> /etc/fstab'
```
