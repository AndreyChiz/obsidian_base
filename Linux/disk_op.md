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



#### Добавление места

```shell
NAME                    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0                     7:0    0 91,9M  1 loop /snap/lxd/24061
loop1                     7:1    0 63,3M  1 loop /snap/core20/1828
loop2                     7:2    0 49,9M  1 loop /snap/snapd/18357
sda                       8:0    0 74,6G  0 disk 
├─sda1                    8:1    0    1M  0 part 
├─sda2                    8:2    0    2G  0 part /boot
└─sda3                    8:3    0 72,6G  0 part 
  └─ubuntu--vg-ubuntu--lv
                        253:0    0 36,3G  0 lvm  /
sdb                       8:16   0 57,3G  0 disk 
```

`sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv`: на всё свободное
`sudo vgextend ubuntu-vg /dev/sdb`: добавление в группу нового раздела
`sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv`



