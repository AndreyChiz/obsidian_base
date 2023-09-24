https://www.youtube.com/watch?v=fJ2i0IWQdLA
### Установка
`sudo apt install net-tools curl dnsutils htop pwgen wget nmon git`

##### Docker (docker engine)
doc  https://docs.docker.com/engine/install/ubuntu/
````console
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
````

##### Docker Compose
doc https://docs.docker.com/compose/install/standalone/
```shel
sudo curl -SL https://github.com/docker/compose/releases/download/v2.20.3/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose

docker-compose version
```

```shel
sudo apt install python3-pip
```

##### Ngnix proxy manager


