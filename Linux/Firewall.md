```bash



sudo apt update
sudo apt install ufw

sudo ufw allow 80/tcp

sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw allow ftp
sudo ufw allow smtp
sudo ufw allow dns
sudo ufw allow ntp

sudo ufw status
sudo ufw status numbered
sudo ufw status verbose : какими сетями управляет

sudo ufw app list
sudo ufw default deny incoming
sudo ufw enable
sudo ufw reload
```


`cd /etc/ufw/applications.d`:   файлы конфигурации приложений
`sudo ufw  allow 'nginx Full'`: пример


пример файла
```nginx
[Nginx HTTP]
title=Web Server (Nginx, HTTP)
description=Small, but very powerful and efficient web server
ports=80/tcp

[Nginx HTTPS]
title=Web Server (Nginx, HTTPS)
description=Small, but very powerful and efficient web server
ports=443/tcp

[Nginx Full]
title=Web Server (Nginx, HTTP + HTTPS)
description=Small, but very powerful and efficient web server
ports=80,443/tcp



```