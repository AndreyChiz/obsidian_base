https://www.youtube.com/watch?v=1sF42xKL7tA

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
