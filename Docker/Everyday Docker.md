`sudo systemctl stop docker docker.socket containerd` - остановка нетивного сервиса docker
`sudo systemctl disable docker docker.socket containerd` - отключение автозагрузки нетивного сервиса

`docker context ls`: список контекста docker 
```shel
docker context ls
NAME            DESCRIPTION                               DOCKER ENDPOINT                                  ...
default *       Current DOCKER_HOST based configuration   unix:///var/run/docker.sock                      ...
desktop-linux                                             unix:///home/<user>/.docker/desktop/docker.sock  ...        
```

----

Выбор  хоста к которому подключается docker cli (клиент)
```bash
docker context use default
default
Current context is now "default"
```
