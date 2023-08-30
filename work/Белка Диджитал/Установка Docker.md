
   
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



Теперь Docker установлен и готов к использованию на удаленном сервере. Не забудьте добавить своего пользователя в группу `docker`, чтобы избежать необходимости использовать `sudo` при работе с Docker:

```sh
sudo usermod -aG docker username
```

После этого перезайдите на сервер или выполните `newgrp docker`, чтобы изменения вступили в силу.