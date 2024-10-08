### Настройка

выставил в биосе режим s3
открыл в nat 9 порт на роутере

```bash 
.bashrc
alias my_server_connect='ssh -p 050286 c2h5oh@192.168.1.68'
alias my_server_internet_connect='ssh -p 050286 c2h5oh@89.179.72.30'
alias my_server_up='wakeonlan -i 192.168.1.68 00:1d:60:17:5c:dc'
alias my_server_local_up='wakeonlan  00:1d:60:17:5c:dc'
alias my_server_internet_up='wakeonlan -i 89.179.72.30 00:1d:60:17:5c:dc'
```


#### Сервер

`sudo apt update sudo apt install ethtool`

`sudo ethtool <имя_интерфейса> | grep "Wake-on"`
Если вы видите "Wake-on: g" (где g - это magicpacket), это означает, что WOL поддерживается.
Создайте скрипт для настройки WOL и добавьте его в автозагрузку. Создайте новый файл с расширением `.service` в директории `/etc/systemd/system/`. Например, `/etc/systemd/system/wol.service`. Откройте этот файл в текстовом редакторе и добавьте следующее содержимое:
```  sh
[Unit]
Description=Enable Wake-on-LAN

[Service]
Type=oneshot
ExecStart=/sbin/ethtool -s enp3s0 wol g

[Install]
WantedBy=basic.target
```

`sudo ethtool -s enp3s0 wol g` 




- `g`: Это значение режима для WoL, которое означает "гигабитный режим". Это позволяет сетевой карте оставаться активной в режиме гигабитной скорости и принимать пакеты WoL.

Другие возможные значения режима WoL включают:

- `p`: Режим "магистрального трафика". Этот режим позволяет сетевой карте оставаться активной только для трафика, который адресован ей напрямую. Это может быть полезным, если вы хотите активировать компьютер с помощью WoL, но не хотите, чтобы сетевая карта оставалась активной для всего трафика.
    
- `u`: Режим "широковещательного трафика". Этот режим позволяет сетевой карте оставаться активной только для широковещательных пакетов (broadcast). Это также может быть полезно для активации компьютера с помощью WoL, но оставить сеть более безопасной.


```shell
sudo systemctl daemon-reload
sudo systemctl enable wol.service
```

#### Клиент
`sudo apt update`
`sudo apt install wakeonlan`
`wakeonlan 00:1d:60:17:5c:dc`

``` shell
ethtool <имя_сетевого_интерфейса> | grep Wake-on

Supports Wake-on: pumbg
	Wake-on: g
	Current message level: 0x00000033 (51)
			       drv probe ifdown ifup
	Link detected: yes
```

Символы после "Supports Wake-on" и "Wake-on" предоставляют информацию о режимах поддержки WOL. В данном случае:

- `p` означает, что поддерживается режим WOL с использованием пакетов электропитания (Power Management).
- `u` означает, что поддерживается режим WOL по событиям USB (USB Wake-up).
- `m` означает, что поддерживается режим WOL при изменении состояния сетевого кабеля (Magic Packet).
- `b` означает, что поддерживается режим WOL с использованием широковещательных пакетов (Broadcast).
- `g` означает поддержку гибридного режима WOL, который объединяет различные способы активации WOL.