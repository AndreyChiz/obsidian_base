

### Старт стоп 

`docker ps -a`: список всех контейнеров
`docker context list`
`docker images`
`docker run -it busybox` : -it интерактивный терминал
(в busybox команда при старте образа `sh` ,  по этому после старта образа подключаемся к запущенной команде)
 `#hostname`: имя контейнера
 `#hostname - i`: IP контейнера
`docker container prune` удаление всех запущенных контейнеров
`docker run -d nginx`: -d запуск в фоне

`docker run `: каждый раз создает новый контейнер, старые остаются остановленными

`docker container  inspect 898b3b858c79`: отобразить информацию по контейнер
`docker container  inspect 898b3b858c79 | grep IPAddress`:  отфильтровать ip контейнера

`docker stop id`
`docker kill`

`docker exec -it name_container bash `    : exec запустить процесс внутри контейнера
`exec`
*(docker exec -it stupefied_murdock bash)*

`docker run -d --name my_ngonx nginx`: имя для контейнера
`--name`


### Меппинг портов

`docker rub -p 8080:80 --name xxx nginx` : внешний порт:внутренний порт
`-p 8080:80`
`docker run -d -p 8080:80 --name xxx nginx`


### Меппинг томов

`docker run -v <путь локальной папки>:<путь папки в контейнере> <имя контейнера>`: при этом содержимое папки внутри контейнера заменится содержимым локальной папки
`${pwd}`: путь текущей локальной папки