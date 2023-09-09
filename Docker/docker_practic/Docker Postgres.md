


```yaml
  postgres:  
    container_name: db  
    restart: always  
    image: postgres  
    environment:  
      - POSTGRES_USER=${DB_USER}  
      - POSTGRES_PASSWORD=${DB_PASSWORD}  
      - POSTGRES_DB=${DB}  
    volumes:  
      - ./postgres-data:/var/lib/postgresql/data  
#    ports:  
#      - "5432:5432"
```

внутри контейнера "localhost" означает сам контейнер, а не хостовую машину.

```sh
docker run --name belka_test_postgres -e POSTGRES_PASSWORD=1 -p 5432:5432 -d postgres
```

первый - порт машины, второй порт контейнера


подключиться к базе данных с помощью любого клиента PostgreSQL, используя IP-адрес сервера и порт, который вы указали при запуске контейнера.

   Остановить контейнер:

   ```sh
   docker stop your_postgres_container_name
   ```

   Удалить контейнер (после его остановки):

   ```sh
   docker rm your_postgres_container_name
   ```

Обратите внимание, что данные, созданные внутри контейнера, будут потеряны после его удаления. Если вам нужно сохранить данные, рассмотрите возможность использования Docker volumes для хранения данных базы данных за пределами контейнера.

Эти шаги помогут вам развернуть контейнер с PostgreSQL при использовании Docker.

