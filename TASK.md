```shell
# базовые
sudo systemctl set-default multi-user.target
echo "%sudo   ALL=(ALL:ALL) NOPASSWD: ALL" | sudo tee -a /etc/sudoers
echo 'HISTSIZE=1000' > ~/.bashrc
echo 'HISTFILESIZE=2000' >> ~/.bashrc
echo 'HISTCONTROL=ignoredups' >> ~/.bashrc
echo 'HISTTIMEFORMAT="%Y-%m-%d %H:%M:%S "' >> ~/.bashrc
echo 'PROMPT_COMMAND="history -a; $PROMPT_COMMAND"' >> ~/.bashrc
source ~/.bashrc

# настройка резервного копирования
# Создание скрипта резервного копирования с именем, основанным на дате

sudo bash -c 'echo "#!/bin/bash" > /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "SOURCE_DIR=\"/\"  # Если вы хотите скопировать всю систему, оставьте так" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "BACKUP_ROOT=\"/backup_hdd\"" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "DATE=\$(date +\"%Y-%m-%d_%H-%M-%S\")" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "BACKUP_DIR=\"\$BACKUP_ROOT/backup_\$DATE\"" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "EXCLUDE_DIRS=\"/backup_hdd /some_hdd /swap.img\"" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "mkdir -p \$BACKUP_DIR" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "rsync -av --delete --compress --info=progress2 --exclude=\$EXCLUDE_DIRS \$SOURCE_DIR/ \$BACKUP_DIR/" >> /usr/local/bin/backup_system.sh'
sudo chmod +x /usr/local/bin/backup_system.sh


# Создание скрипта восстановления
sudo bash -c 'echo "#!/bin/bash" > /usr/local/bin/restore_system.sh'
sudo bash -c 'echo "BACKUP_DIR=\"/backup_hdd/full_system_backup\"" >> /usr/local/bin/restore_system.sh'
sudo bash -c 'echo "TARGET_DIR=\"/\"  # Восстанавливайте в нужное место" >> /usr/local/bin/restore_system.sh'
sudo bash -c 'echo "rsync -av --info=progress2 \$BACKUP_DIR \$TARGET_DIR" >> /usr/local/bin/restore_system.sh'
sudo chmod +x /usr/local/bin/restore_system.sh

# Добавление алиасов в ~/.bashrc
sudo bash -c 'echo "alias backup_system=\"sudo backup_system.sh\"" >> ~/.bashrc'
sudo bash -c 'echo "alias restore_system=\"sudo restore_system.sh"" >> ~/.bashrc'
source ~/.bashrc




sudo localedef ru_RU.UTF-8 -i ru_RU -fUTF-8; export LANGUAGE=ru_RU.UTF-8; \
export LANGUAGE=ru_RU.UTF-8; \
export LANG=ru_RU.UTF-8; \
export LC_ALL=ru_RU.UTF-8; \
sudo dpkg-reconfigure locales
# убираем всё галочки кроме ru_RU.UTF-8 UTF-8
# на втором экране выбираем то-же

# Настройка openssh-server
sudo nano /etc/ssh/sshd_config
# #Include /etc/ssh/sshd_config.d/*.conf
# PermitRootLogin no
# PubkeyAuthentication yes
# PasswordAuthentication no
# Match User c2h5oh
# PasswordAuthentication yes
# PasswordAuthentication no


# Настройки админа
# выйти из ssh и со своей машины выполнить 
	ssh-copy-id -p 050286 c2h5oh@192.168.1.68

# Настройка пользователя
sudo useradd -m -s /bin/bash www
sudo passwd www
sudo usermod -aG cdrom www 
sudo usermod -aG sudo www 
sudo usermod -aG dip www 
sudo usermod -aG plugdev www 
sudo usermod -aG lxd www 
sudo passwd www











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