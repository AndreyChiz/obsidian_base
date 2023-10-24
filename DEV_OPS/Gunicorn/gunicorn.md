
wsgi.py
```python
from app import app # импорт приложения из точки входа flask

if __name__ == "__main__":
    app.run()
```

`gunicorn --bind 0.0.0.0:5000 wsgi:app`: запуск

systemctl edit --full [название проекта]

```
  GNU nano 4.8                               /etc/systemd/system/c2h5oh.ddns.net                               Modified  
# Опишем что за сервис
[Unit]
# Описание
Description=Blueoctopus gunicorn instance
# Здесь мы говорим systemd запускать наш сервер только после загрузки сетевых служб. 
After network.target

# Уже описывает наш юнит для системы.
[Service]
# От чьего имени запускать сервис
# Это я
User=www
# Группа созданная для Nginx
Group=www-data
# Где его запускать
WorkingDirectory=/home/www/sites/c2h5oh
# Путь к виртуальному окружению, в котором его запускать
Envirovement="PATH=/home/www/sites/c2h5oh/c2h5oh_env/bin"
# Команда запуска сервиса с параметрами, о ней ниже
ExecStart=/home/www/sites/c2h5oh/c2h5oh_env/bin/gunicorn --workers 2 --bind unix:gunicorn.sock -m 007 wsgi:app

# Здесь опишем на каком уровне стартует наш сервис
[Install]
# Он будет соостветсвовать стандартному серверному (Runlevel 3)
# Многопользовательский режим с поддержкой сети, но без графического интерфейса.
WantedBy=multi-user.target


  


```

`sudo systemctl start [название проекта]`
`sudo systemctl daemon-reload`
`sudo systemctl start dooucofe.ru.service`
`sudo systemctl enable dooucofe.ru.service`
