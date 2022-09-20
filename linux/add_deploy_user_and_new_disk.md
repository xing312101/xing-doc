# Add deploy user and new disk
> 目的：留下amazon/Linux預建的user: ubuntu，後續使用上用user: deploy，另開一個disk去使用空間

```
1.
chown -R ubuntu:ubuntu /ebs60
useradd deploy
passwd deploy
cp -r ubuntu deploy
vim passwd # 為了sudo
vim 90-cloud-init-users # 為了sudo
mv deploy/ /ebs60/
ln -s /ebs60/deploy . # 家目錄link


2.
fdisk -l
mkdir /ebs10
mount /dev/xvdf /ebs10
df -k
mkfs.ext4 /dev/xvdf
mount -t ext4 /dev/xvdf /ebs10
vi /etc/mtab
vi /etc/fstab # 開機預掛
vi /etc/exports # 設定NFS用
```
