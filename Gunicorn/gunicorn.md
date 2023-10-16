
wsgi.py
```python
from app import app # импорт приложения из точки входа flask

if __name__ == "__main__":
    app.run()
```

`gunicorn --bind 0.0.0.0:5000 wsgi:app`: запуск

systemctl edit --full [название проекта]

```
[Unit]
Description=dooucoffe.ru gunicorn instance
After=network.target

[Service]
User=c2h5oh
Group=www-data
WorkingDirectory=/home/c2h5oh/server/code/dooucoffe.ru
Environment="PUTH=/home/c2h5oh/server/code/dooucoffe.ru/venv/bin"
ExecStart=/home/c2h5oh/server/code/dooucoffe.ru/venv/bin/gunicorn -w 9 -b unix:gunicorn.sock -m 007  wsgi:app

[Install]
WantedBy=multy-user.target  


```

`sudo systemctl start [название проекта]`
`sudo systemctl daemon-reload`
`sudo systemctl start dooucofe.ru.service`
`sudo systemctl enable dooucofe.ru.service`
