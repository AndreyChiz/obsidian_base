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

`SELECT cron.unschedule(1);`: удалить задачу с id 1 из списка задач 


![[Pasted image 20230831105432.png]]


список хранимых процедур
```sql
SELECT routine_name
FROM information_schema.routines
WHERE routine_type = 'PROCEDURE'
ORDER BY routine_name;

```

```sql
SELECT proname, prorettype::regtype, proargnames, proargtypes::regtype[], proargmodes
FROM pg_proc
WHERE pronamespace = 'public'::regnamespace;
```


Хранимая процедура
```
CREATE OR REPLACE PROCEDURE belka_rundom_data_value() AS
$$
DECLARE
    random_value DOUBLE PRECISION;
BEGIN
    random_value := random() * 10; 
    INSERT INTO belka_test_table (time, value)
    VALUES (CURRENT_TIMESTAMP, random_value);
END;
$$ LANGUAGE plpgsql;
```


`CALL belka_rundom_data_value();` : Вызов хранимой процедуры


 `'*/5 * * * *'`:
1. **Минуты (`*`):**
   В первом поле, `*` означает "каждое значение". Таким образом, задание будет выполняться на любой минуте.

2. **Часы (`*/5`):**
   Во втором поле, `*/5` означает "каждый пятый час". Это означает, что задание будет выполняться на каждом пятом часе.

3. **Дни месяца (`*`):**
   В третьем поле, `*` означает "каждое значение". Задание будет выполняться в любой день месяца.

4. **Месяцы (`*`):**
   В четвертом поле, `*` означает "каждое значение". Задание будет выполняться в любом месяце.

5. **Дни недели (`*`):**
   В пятом поле, `*` означает "каждое значение". Задание будет выполняться в любой день недели.

Таким образом, выражение `'*/5 * * * *'` переводится как "каждые 5 часов". В данном контексте, задание будет выполняться каждый раз, когда наступает час, который делится на 5 (5:00, 10:00, 15:00 и так далее).

Помните, что выражения cron используются для задания времени выполнения задач на основе определенных интервалов. Перед использованием регулярных задач, убедитесь, что вы понимаете, как работают выражения cron, и какие интервалы вам нужны для вашего конкретного случая.

````sql
SELECT cron.schedule('*/1 * * * *', 'CALL insert_random_data();');
````

`SELECT cron.job_run(job_id);`: запуск выполнения задач

`SELECT cron.schedule('*/1 * * * *', 'CALL belka_recursive_function();');`