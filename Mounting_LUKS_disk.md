# Decrypting and mounting LUKS volume

1. Live boot VM using ParrotOS
2. get root
   a. sudo su
3. list volumes
   a. lsblk
4. unlock volume
   a. udisksctl unlock -b /dev/sda5
5. list volumes
   a. lsblk
6. mount the drive
   a. udisksctl mount -b /dev/mapper/hostname--vg-root
7. remove password
   a. vi /media/root/9441abcd-1a1a-b2b2-95ba3e14d9a/etc/shadow
   b. remove the hash from /etc/shadow
