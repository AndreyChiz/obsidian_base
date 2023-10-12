```shell
sudo systemctl set-default multi-user.target # переключем в режим командной строки
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
echo "%adm ALL=(ALL:ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
%adm ALL=(ALL:ALL) NOPASSWD:ALL # отменить ввод пароля для пользователей группы adm при действии от sudo

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