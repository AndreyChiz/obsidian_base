### OpenSSH сервер

#### Установка
```sh
sudo apt install openssh-server -y #установка
sudo systemctl enable ssh # добавить в автозагрузку
ssh localhost #проверка работоспособности
```

#### Настройка
```sh
# создание бекапа
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.factory-defaults

# настройка портов
sudo vi /etc/ssh/sshd_config 
# Port раскомментировать строку 
# заменить на Port 12345
# PermitRootLogin no
# PubkeyAuthentication yes
sudo systemctl restart ssh
# перезагрузиться
sudo ip a # узнать ip, он будет там где то)
sudo systemctl status ssh # проверить статус
```

### Подключение
```sh
ssh c2h5oh@IP_виртуальной_машины
```

#### Операции
##### Копировыние файлов
`scp /путь/к/локальному/файлу имя_пользователя@IP_удаленного_сервера:/путь/на/удаленном/сервере` 

