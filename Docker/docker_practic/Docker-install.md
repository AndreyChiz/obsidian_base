   внутри контейнера "localhost" означает сам контейнер, а не хостовую машину.
   ```sh
   ssh username@remote_server_ip
   ```

   ```sh
  sudo apt install apt-transport-https ca-certificates curl software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  sudo apt update
  sudo apt install docker-ce -y
   ```

   ```sh
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

добавить пользователя в группу `docker`, чтобы  без  `sudo` 

```sh
sudo usermod -aG docker username
```

`$USER`
 
`newgrp docker`, чтобы изменения вступили в силу.