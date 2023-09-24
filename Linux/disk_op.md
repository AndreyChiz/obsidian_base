`lsblk` информация по дискам
`sudo fdisk -l /dev/sda`: подробно
`df -T`: информация по смонтированным устройствам (посмотреть файловую систему)
`du -sh *`: размер всех файлов

#### Монтирование
`sudo mkdir /mnt/mydisk`
`sudo mount /dev/sda /mnt/mydisk`
`cd /mnt/mydisk`

`sudo umount /mnt/mydisk`

##### Чтобы монтирование сохранялось
`sudo nano /etc/fstab`
`/dev/sdb1 /mnt/mydata ext4 defaults 0 0`
`sudo mount -a`: монтировать всё из файла


#### Форматирование

 
`sudo mkfs.ext4 /dev/sda`
`sudo mkfs.xfs /dev/sda`

`sudo apt-get install ntfs-3g` ntfs
`sudo mkntfs /dev/sdX`
`sudo mkfs.exfat /dev/sdX




