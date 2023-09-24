```shell
sudo apt update
sudo apt upgrade
echo "%adm ALL=(ALL:ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
echo "blacklist floppy" | sudo tee /etc/modprobe.d/blacklist-floppy.conf
sudo rmmod floppy
sudo update-initramfs -u
mkdir disk_d
sudo nano /etc/fstab
sudo mkfs.ext4 /dev/sdb
#> /dev/sdb /home/c2h5oh/disk_d ext4 defaults 0 0
sudo mount -a
df -T
sudo apt install timeshift
sudo timeshift --create --debug
sudo nano /etc/timeshift.json
# изменить место для хранения образов в первой строке
# sudo blkid
sudo apt-get install nvidia-340
nvidia-smi
sudo systemctl set-default multi-user.target
sudo apt install openssh-server
ssh-copy-id -f c2h5oh@192.168.1.68 
sudo apt install lm-sensors
sudo sensors-detect
sensors









```