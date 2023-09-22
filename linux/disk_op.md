`lsblk` информация по дискам
`sudo fdisk -l /dev/sda`: подробно
`df -T`: информация по смонтированным устройствам (посмотреть файловую систему)

#### Монтирование
`sudo mkdir /mnt/mydisk`
`sudo mount /dev/sda /mnt/mydisk`
`cd /mnt/mydisk`

`sudo umount /mnt/mydisk`

#### Форматирование

 
`sudo mkfs.ext4 /dev/sda`
`sudo mkfs.xfs /dev/sda`

`sudo apt-get install ntfs-3g` ntfs
`sudo mkntfs /dev/sdX`
`sudo mkfs.exfat /dev/sdX




