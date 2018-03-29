# rpi-bk
raspberry pi 3b stretch backup to local img file 

script modifed from https://github.com/conanwhf/RaspberryPi-script/blob/master/rpi-backup.sh
thanks to conanwhf!

Tested on my raspberry pi 3b with stretch having docker, hass.io, homebridge installed.

the idea is simple, from original conanwhf.
1. create a .img file smaller than actual tf card size. actually used storage*1.5
2. part img file to 2 partitions. 1 boot, 1 root and mount them.
3. fill img file using rsync
4. copy the img file to anywhere you like! you can then compress it to save space!

note:
1. create img file to local folder /mnt
you can change it to any folder or usb device mounted folder, do not change to ftp mounted folder using curlftpfs. I have tested it and it is not working. Problem is that it fails to mount img file from ftp folder mounted using curlftpfs.
2. default img size is 1.5 larger than what is actually used on /dev/root and /dev/boot. eg. I use `df -P` and get 6.9GB used. but actual file copied to img file is 9GB by mounting img file and using `df -P` on the img file. After I restore this img file to a new tf card. I get 7.7GB using `df -P`.  I am confused. So I set 1.5 to make sure rsync works correctly. 
3. After img file is created, you can copy it to a usb drive or a NAS. 
