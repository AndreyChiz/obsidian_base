
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.6/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo docker–compose version
```



- `docker-compose down`: Останавливает и удаляет все контейнеры, созданные с помощью
- `docker-compose down --rmi all` : Удалить все образы, связанные с вашими контейнерами
- `docker image prune -a` : удалите оставшиеся образы после удаления контейнеров
- `docker rmi dpage/pgadmin4 postgres`: Удалить конкретный образ

- `docker-compose up -d`: Запуск контейнеров в фоновом режиме.
- `docker-compose up`.

- `docker-compose ps`: Показывает статус запущенных контейнеров.
- `docker-compose logs`: Отображает журналы (логи) контейнеров.
- ` docker-compose up --foece-recreate`: пересоздание при изменении



```yaml
version: '3'
services:
  postgres:
    container_name: postgres_container
    image: postgres
    environment:
      POSTGRES_PASSWORD: 1
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/container_data/postgres

  pgadmin:
    container_name: pgadmin_container
    image: dpage/pgadmin4
    environment:
      PGADMIN_DEFAULT_EMAIL: your_email@example.com
      PGADMIN_DEFAULT_PASSWORD: your_pgadmin_password
    ports:
      - "5050:80"
    volumes:
      - pgadmin_data:/container_data/pgadmin

volumes:
  postgres_data:
  pgadmin_data:
```




