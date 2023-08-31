установка внутри контейнера

`docker exec -it postgres_container bash` :  консоль контейнера
`psql -U postgres -c "SELECT version();"` : версия postgres

```bash
                                                       version                  
                                     
--------------------------------------------------------------------------------
-------------------------------------
 PostgreSQL 15.4 (Debian 15.4-1.pgdg120+1) on x86_64-pc-linux-gnu, compiled by g
cc (Debian 12.2.0-14) 12.2.0, 64-bit
(1 row)
```

версия 15

```bash
apt-get update
apt-get install postgresql-13-cron
```

после установки перезапустить контейнер

`docker-compose restart`

`cd /var/lib/postgresql/data/`

`apt install nano`

`nano postgresql.conf `

```
shared_preload_libraries = 'pg_cron'    # (change requires restart)
cron.database_name = 'postgres'

```

`psql -U postgres`

`CREATE EXTENSION pg_cron;`

`SELECT extname, extversion FROM pg_extension WHERE extname = 'pg_cron';` : версия

`DROP EXTENSION IF EXISTS pg_cron;` : удалить расширение

`SELECT * FROM cron.job;` : список задач


![[Pasted image 20230831105432.png]]


