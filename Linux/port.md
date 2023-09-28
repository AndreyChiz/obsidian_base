8/13.1
`sudo lsof -i :5432`: что использует данный
`nc -zv 192.168.1.100 80`: проверить доступность порта не соединяться

##### Отправка сообщений
`sudo apt-get install netcat-traditional`
`echo -n "Сообщение по tcp" | nc 89.179.72.30 9`: tcp

`sudo apt-get install socat`
`cho -n "Ваше сообщение" | socat - UDP4-DATAGRAM:192.168.1.68:80`
`echo -n "Ваше сообщение" | socat - TCP:хост_назначения:порт`

#### Прослушивание портов
`sudo nc -l -p 8` : tcp

`sudo tcpdump -i enp3s0 -nn -X udp port 9`
`sudo tcpdump -i enp3s0 -nn -X tcp port 9`




`sudo socat UDP-LISTEN:9 -`



`kill -15 <PID>`:  soft
`kill -9 <PID>`: hard


