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

sudo nano /etc/systemd/system/wol.service
#------------                    
[Unit]
Description=Enable Wake-on-LAN

[Service]
Type=oneshot
ExecStart=/sbin/ethtool -s enp3s0 wol g

[Install]
WantedBy=basic.target
#-------------
sudo systemctl daemon-reload
sudo systemctl enable wol.service
sudo systemctl start

<<<<<<< HEAD
=======

>>>>>>> origin/main
sudo apt install wakeonlan
wakeonlan 00:1d:60:17:5c:dc

sudo apt update
sudo apt install ufw
sudo ufw allow 50286/tcp
sudo ufw enable
sudo ufw allow http
sudo ufw allow https

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
sudo systemctl enable docker.service
sudo systemctl enable containerd.service

sudo curl -SL https://github.com/docker/compose/releases/download/v2.20.3/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

```





```bash
docker run -d --network=my_network -p 8880:80 -p 8443:443 -p 8881:81 your_image

```