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
# exit
# sudo reboot




```