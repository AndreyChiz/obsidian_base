```shell
#---------------------------------------------------------------
# базовые
sudo systemctl set-default multi-user.target
echo "%sudo   ALL=(ALL:ALL) NOPASSWD: ALL" | sudo tee -a /etc/sudoers
source ~/.bashrc
df -h 
#---------------------------------------------------------------
#Проверка системы
sudo systemctl status #проверка состояния
sudo apt update
sudo apt upgrade
sudo journalctl -b -p err #посмотреть какие ошибки есть при загрузке

#----------------------------------------------------------------

# Настройка локали
sudo localedef ru_RU.UTF-8 -i ru_RU -fUTF-8; export LANGUAGE=ru_RU.UTF-8; \
export LANGUAGE=ru_RU.UTF-8; \
export LANG=ru_RU.UTF-8; \
export LC_ALL=ru_RU.UTF-8; \
sudo dpkg-reconfigure locales
# убираем всё галочки кроме ru_RU.UTF-8 UTF-8
# на втором экране выбираем то-же
#-------------------------------------------------------------
# Настройка openssh-server
sudo nano /etc/ssh/sshd_config
# #Include /etc/ssh/sshd_config.d/*.conf
# PermitRootLogin no
# PubkeyAuthentication yes
# PasswordAuthentication yes
# Match User c2h5oh
# PasswordAuthentication yes
# PasswordAuthentication no

# Настройки админа
# выйти из ssh и со своей машины выполнить 
ssh-copy-id -p 050286 c2h5oh@192.168.1.68
#-------------------------------------------------------------
Внутренний пользователь сервера
# Настройка пользователя
sudo useradd -m -s /bin/bash www
sudo passwd www #ast10273
sudo usermod -aG cdrom www 
sudo usermod -aG sudo www 
sudo usermod -aG dip www 
sudo usermod -aG plugdev www 
sudo usermod -aG lxd www 
sudo passwd www
# ---------------------------------------------------
# Установка настройка timeshift
sudo apt install timeshift
timeshift --create --comments "install"
sudo nano /etc/timeshift.json
{
  "backup_device_uuid" : "f2296b99-6525-49b7-8426-024ae6840199",
  "parent_device_uuid" : "",
  "do_first_run" : "false",
  "btrfs_mode" : "false",
  "include_btrfs_home_for_backup" : "false",
  "include_btrfs_home_for_restore" : "false",
  "stop_cron_emails" : "true",
  "btrfs_use_qgroup" : "true",
  "schedule_monthly" : "false",
  "schedule_weekly" : "false",
  "schedule_daily" : "true",
  "schedule_hourly" : "false",
  "schedule_boot" : "false",
  "count_monthly" : "2",
  "count_weekly" : "3",
  "count_daily" : "5",
  "count_hourly" : "6",
  "count_boot" : "5",
  "snapshot_size" : "4982275706",
  "snapshot_count" : "96430",
  "date_format" : "%Y-%m-%d %H:%M:%S",
  "exclude" : [
        "/swap.img",
        "swap.img"      
  ],
  "exclude-apps" : [
        "swap.img"
  ]
}
#--------------------------------------------------
#Настройка часовог пояса
sudo timedatectl set-timezone Europe/Astrakhan
timedatectl
sudo systemctl restart systemd-timesyncd
#--------------------------------------------------
# Установка NGINX
wget https://nginx.org/download/nginx-1.25.2.tar.gz
cd ng*
tar xvf nginx-*

./configure --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --pid-path=/var/run/nginx.pid --user=www-data --group=www-data 













 # переключем в режим командной строки
sudo systemctl status #проверка состояния
sudo apt update
sudo apt upgrade
sudo journalctl -b -p err #посмотреть какие ошибки есть при загрузке
#(ошибка флопи) окт 11 16:27:19 astmark10274 kernel: blk_update_request: I/O error, dev fd0, sector 0 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 0
# (решение) 
# sudo su
# sudo echo "blacklist floppy" >> /etc/modprobe.d/blacklist-floppy.conf
# sudo modprobe -r floppy
# echo 'KERNEL=="fd0", ENV{UDISKS_IGNORE}="1"' | sudo tee /etc/udev/rules.d/10-local.rules
#KERNEL=="fd0", ENV{UDISKS_IGNORE}="1"
# exit
# sudo reboot
echo "%adm ALL=(ALL:ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers %adm ALL (ALL:ALL) NOPASSWD:ALL # отменить ввод пароля для пользователей группы adm при действии от sudo

#Настройка WOL
sudo apt install ethtool
sudo nano /etc/systemd/system/wol.service
#Вставить в файл следующий текст:
#[Unit]
#Description=Enable Wake-on-LAN

#[Service]
#Type=oneshot
#ExecStart=/sbin/ethtool -s enp3s0 wol g

#[Install]
#WantedBy=basic.target
sudo systemctl daemon-reload
sudo systemctl enable wol.service



#Настроить UFW


```