! не может обрабатывать динамический контент (python app)
#### Конфигурация
`/etc/nginx/nginx.conf`: базовая конфигурация
`include /etc/nginx/conf.d/*.conf`: подключение доп. конфигураций
nginx сначала читает базовую кнфигурацию, потом читает конфиги из папки conf.d  если встречаются одинаковые директивы то перезаписывает, разные добвляет


` server {}`: блок в котором прописывают директивы (listen, server_name)


`sudo nginx -t`:  проверка конфигураций
`nginx -V 2>&1 | grep -o with-openssl[^\ ]*` : Версия openssl



`service nginx reload`

``` sh
sudo nano /etc/nginx/nginx.conf
```

```nginx
user www-data;               # Пользователь, от имени которого запускается Nginx.
worker_processes auto;       # Количество рабочих процессов автоматически определяется.

pid /run/nginx.pid;          # Путь к файлу, в котором будет храниться идентификатор процесса Nginx.

events {
    worker_connections 1024; # Максимальное количество одновременных соединений для каждого рабочего процесса.
    multi_accept on;         # Разрешает одновременное принятие нескольких соединений.
    use epoll;               # Использует механизм epoll для обработки событий.
}
http {
    include /etc/nginx/mime.types;        # Включает файл с типами контента (mime.types).
    default_type application/octet-stream; # Задает тип контента по умолчанию.

    access_log /usr/local/nginx/logs/access.log;  # Путь к файлу журнала доступа.
    error_log /usr/local/nginx/logs/error.log;    # Путь к файлу журнала ошибок.


    sendfile on;           # Включает использование системного вызова sendfile для увеличения производительности.
    tcp_nopush on;         # Включает опцию TCP_NOPUSH для передачи данных клиенту без задержек.
    tcp_nodelay on;        # Включает опцию TCP_NODELAY для минимизации задержек в передаче данных.
    keepalive_timeout 65;  # Время ожидания keep-alive соединений.

    types_hash_max_size 2048; # Максимальный размер хэш-таблицы для определения типов контента.

    server_tokens off;   # Отключает отображение версии Nginx в HTTP-заголовках.

    gzip on;                    # Включает сжатие (gzip).
    gzip_comp_level 6;          # Устанавливает уровень сжатия.
    gzip_min_length 1000;       # Минимальная длина файла для сжатия.
    gzip_proxied any;           # Сжимает данные для всех клиентов, включая прокси.
    gzip_types text/plain text/css application/json application/javascript application/xml application/xml+rss application/x-javascript application/x-font-ttf font/opentype image/svg+xml image/x-icon;

    client_max_body_size 10M;    # Максимальный размер загружаемых файлов.
    client_body_buffer_size 128k; # Размер буфера для данных клиента.

    include /etc/nginx/conf.d/*.conf;    # Включает дополнительные конфигурационные файлы.
    include /etc/nginx/sites-enabled/*;   # Включает конфигурации сайтов.

    # SSL/TLS настройка
    ssl_protocols TLSv1.2 TLSv1.3;                # Задает протоколы SSL/TLS.
    ssl_prefer_server_ciphers off;               # Отключает предпочтение серверных шифров.
    ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH'; # Задает шифры.
    ssl_session_timeout 1d;                    # Устанавливает время хранения сессий SSL.
    ssl_session_cache shared:SSL:50m;          # Устанавливает кэш сессий SSL.
    ssl_stapling on;                           # Включает механизм SSL-степлинга.
    ssl_stapling_verify on;                    # Включает проверку SSL-степлинга.

    # Оптимизация производительности
    fastcgi_cache_path /var/cache/nginx levels=1:2 keys_zone=my_cache:10m; # Задает путь и параметры кэша FastCGI.
    fastcgi_cache_key "$scheme$request_method$host$request_uri";       # Задает ключ для кэширования.

    # Защита от атак
    limit_req_zone $binary_remote_addr zone=one:10m rate=5r/s; # Устанавливает ограничение на скорость запросов.



    # Логирование ошибок и доступа
    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                  '$status $body_bytes_sent "$http_referer" '
                  '"$http_user_agent"';
}
```

```sh
sudo mkdir -p /var/cache/nginx
sudo mkdir /etc/nginx/conf.d/

```


```sh
sudo nano /etc/nginx/proxy_params
```

```nginx
proxy_set_header Host $http_host;              # Устанавливает заголовок "Host" равным значению из запроса.
proxy_set_header X-Real-IP $remote_addr;      # Устанавливает заголовок "X-Real-IP" равным IP-адресу клиента.
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  # Устанавливает заголовок "X-Forwarded-For" для передачи информации о клиенте и прокси.
proxy_set_header X-Forwarded-Proto $scheme;   # Устанавливает заголовок "X-Forwarded-Proto" равным значению протокола (HTTP или HTTPS).

```

`/usr/local/nginx`


```sh
sudo nano /etc/nginx/sites-available/c2h5oh
```

```ndinx
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name your_domain.com;  # Замените на ваш домен или IP-адрес

    location / {
        include /etc/nginx/proxy_params;  # Используем параметры прокси из созд>
        proxy_pass http://unix:/home/www/sites/c2h5oh/myapp.sock;
       # proxy_pass http://unix:/путь/к/сокету;
    }
    
     location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 30d;
        add_header Cache-Control "public, max-age=2592000";
    }
}


```


```sh
sudo nginx -s reload
```