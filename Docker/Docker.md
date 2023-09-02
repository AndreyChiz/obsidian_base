   внутри контейнера "localhost" означает сам контейнер, а не хостовую машину.
   ```sh
   ssh username@remote_server_ip
   ```

   ```sh
   sudo apt update
   sudo apt install docker.io
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