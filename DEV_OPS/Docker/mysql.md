
```bash
$ docker-compose up -d

# To Tear Down
$ docker-compose down --volumes
```

```yaml
version: '3'

services:
  # Database
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    networks:
      - procapitall_api


networks:
  procapitall_api:
    driver: bridge
volumes:
  db_data:
```