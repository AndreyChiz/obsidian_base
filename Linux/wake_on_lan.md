### Настройка
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
ExecStart=/sbin/ethtool -s <имя_интерфейса> wol g

[Install]
WantedBy=basic.target
```

```shell
sudo systemctl daemon-reload
sudo systemctl enable wol.service
```

#### Клиент
`sudo apt update`
`sudo apt install wakeonlan`
`wakeonlan 00:1d:60:17:5c:dc`

```shell
enp3s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500 inet 192.168.1.68 netmask 255.255.255.0 broadcast 192.168.1.255 inet6 fe80::21d:60ff:fe17:5cdc prefixlen 64 scopeid 0x20<link> ether 00:1d:60:17:5c:dc txqueuelen 1000 (Ethernet) RX packets 925 bytes 276195 (276.1 KB) RX errors 0 dropped 0 overruns 0 frame 0 TX packets 670 bytes 106037 (106.0 KB) TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0
```
