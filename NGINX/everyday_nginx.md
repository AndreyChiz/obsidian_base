! не может обрабатывать динамический контент (python app)
#### Конфигурация
`/etc/nginx/nginx.conf`: базовая конфигурация
`include /etc/nginx/conf.d/*.conf`: подключение доп. конфигураций
nginx сначала читает базовую кнфигурацию, потом читает конфиги из папки conf.d  если встречаются одинаковые директивы то перезаписывает, разные добвляет


` server {}`: блок в котором прописывают директивы (listen, server_name)


`sudo nginx -t`:  проверка конфигураций
`nginx -V 2>&1 | grep -o with-openssl[^\ ]*` : Версия openssl


`sudo nginx -s reload`
`service nginx reload`
/etc/nginx/conf.d/dooucoffe.config 
```conf
server {
        listen 80 default_server
        listen [::]:80 default_server
        server_name c2h5oh.ddns.net www.c2h5oh.ddns.net

        location / {
        include proxy_params
        proxy_pass http://unix/home/c2h5oh/server/code/doucoffe/gunicorn.sock
        }

}
```
`/usr/local/nginx`
/etc/nginx/proxy_params                                
```
proxy_set_header Host $http_host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
```


