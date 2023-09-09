!!!!!!!!!!!!!!!!!!!!!!!!!!`sudo chmod -R 777 /папка с томом pgadmin`


```yaml
pgadmin4:  
    container_name: pgadmin  
    image: dpage/pgadmin4  
    restart: always  
    environment:  
      PGADMIN_DEFAULT_EMAIL: ${USER_EMAIL}  
      PGADMIN_DEFAULT_PASSWORD: ${PGADMIN_PASSWORD}  
      PGADMIN_LISTEN_PORT: 80  # Порт, на котором будет работать pgAdmin  
      PGADMIN_SERVER_MODE: "False"  # Отключение режима сервера, чтобы использовать как клиент  
      PGADMIN_DEFAULT_SERVER: db  # Имя контейнера Postgres  
#      PGADMIN_DEFAULT_SERVER_PORT: 5432  # Порт Postgres  
      PGADMIN_DEFAULT_SERVER_DATABASE: ${DB}  # Имя базы данных  
      PGADMIN_DEFAULT_SERVER_USERNAME: ${USER}  # Пользователь базы данных  
      PGADMIN_DEFAULT_SERVER_PASSWORD: ${PASSWORD}  # Пароль пользователя  
    ports:  
      - "5050:80"  
    volumes:  
      - ./admin/pgadmin-dаta:/var/lib/pgadmin

```


![[Pasted image 20230830210357.png]]


![[Pasted image 20230830210505.png]]