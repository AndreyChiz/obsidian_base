```bash

sudo ufw default deny incoming

sudo apt update
sudo apt install ufw
sudo ufw allow 80/tcp
sudo ufw enable
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw allow ftp
sudo ufw allow smtp
sudo ufw allow dns
sudo ufw allow ntp
sudo ufw status

#~!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
sudo ufw reload

sudo ufw status verbose : какими сетями управляет


```


/etc/ufw/applications   файлы конфигурации приложений

sudo ufw default deny incoming   блокировки входящего трафика по умолчанию: