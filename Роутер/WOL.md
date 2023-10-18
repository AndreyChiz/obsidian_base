ei
У меня получилось заставить работать Wake on Lan на стандартной прошивке:
1. Настроил в веб-панеле переадресацию с внешнего 9 порта на внутренний 9 порт для айпи 192.168.1.254 (Это не закрепленный ни за кем адрес. Настоящий айпи компа - 192.168.1.3)
2. В помощью ssh-доступа, добавил запись в ARP-таблицу: arp -i br0 -s 192.168.1.254 FF:FF:FF:FF:FF:FF (т.е. настроил широковещательную рассылку с незакрепленного ни за кем айпи .254). Взял это отсюда.
https://4pda.to/stat/go?u=https%3A%2F%2Fwiki.dd-wrt.com%2Fwiki%2Findex.php%2F%25D0%2592%25D0%25BA%25D0%25BB%25D1%258E%25D1%2587%25D0%25B5%25D0%25BD%25D0%25B8%25D0%25B5_%25D0%25BF%25D0%25BE_%25D1%2581%25D0%25B5%25D1%2582%25D0%25B8_%25D1%2581_Wake-on-LAN&e=94108557

ssh -oHostKeyAlgorithms=+ssh-dss  -p 22 SuperUser@192.168.1.1
ssh -oHostKeyAlgorithms=+ssh-dss  -p 22 SuperUser@192.168.1.1
SF141FF35697

```sh

sudo apt install sshpass
sshpass -p SF141FF35697 ssh -oHostKeyAlgorithms=+ssh-dss -p 22 SuperUser@192.168.1.1
```

```sh nano router_reboot.sh
```

```sh.sh      
#!/bin/bash

  GNU nano 4.8                                       router_reboot.sh                                                  
password="SF141FF35697"

# Адрес и параметры подключения SSH
ssh_options="-oHostKeyAlgorithms=+ssh-dss -p 22"
ssh_user="SuperUser"
ssh_host="192.168.1.1"

# Команды для выполнения на удаленном хосте
commands=("reset")

# Создаем временный файл с командами
temp_commands_file=$(mktemp)
for command in "${commands[@]}"; do
  echo "$command" >> "$temp_commands_file"
done

# Подключение по SSH и выполнение команд из файла
sshpass -p "$password" ssh $ssh_options $ssh_user@$ssh_host 'bash -s' < "$temp_commands_file"

# Удаляем временный файл
rm -f "$temp_commands_file"
echo "ожидайте настройки ARP для WOL ~ 3 мин"
echo "по окончании настройки будет выведено сообщение"
sleep 180


# Команды для выполнения на удаленном хосте
commands=("arp -i br0 -s 192.168.1.254 FF:FF:FF:FF:FF:FF")

# Создаем временный файл с командами
temp_commands_file=$(mktemp)
for command in "${commands[@]}"; do
  echo "$command" >> "$temp_commands_file"
done

# Подключение по SSH и выполнение команд из файла
sshpass -p "$password" ssh $ssh_options $ssh_user@$ssh_host 'bash -s' < "$temp_commands_file"

# Удаляем временный файл
rm -f "$temp_commands_file"

echo "Настройка ARP закончена можно удвленный WOL активен "

```

```sh
chmod +x router_reboot.sh
touch check_connection.sh
```

```sh
#!/bin/bash

if ping -c 1 -W 5 8.8.8.8 &>/dev/null; then
  echo "Пинг на 8.8.8.8 успешен."
else
  echo "Пинг на 8.8.8.8 не удался. Запуск скрипта для перезагрузки."
  /home/www/script/router_reboot.sh
fi

```

```shell
 chmod +x  check_connection.sh
```

```sh
crontab -e
*/3 * * * * /home/www/script/check_connection.sh

```
