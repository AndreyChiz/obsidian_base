### OpenSSH сервер
https://selectel.ru/blog/ssh-ubuntu-setup/

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
sudo nano /etc/ssh/sshd_config 
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
ssh -p 050286 c2h5oh@192.168.1.68 # с портом

```
##### Ключи RSA
- Генерация ключа
	на клиенте
```sh
ssh-keygen -t rsa
```
- Копирование открытого ключа на удаленный сервер
	на клиенте
```sh 
ssh-copy-id -i ~/.ssh/id_rsa.pub c2h5oh@95.213.154.235
```
_на сервере должен быть пользователь и каталог пользователя_
#### Операции
`scp /путь/к/локальному/файлу имя_пользователя@IP_удаленного_сервера:/путь/на/удаленном/сервере`: копирование 

