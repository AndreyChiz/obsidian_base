Project/python_app/main.py

```python
import calendar  
  
print('Добро пожаловать в календарь')  
  
year =int(input('Введите год: '))  
month = int(input('введите номер месяца: '))  
  
print(calendar.month(year,month))  
  
print('Всё ок!')
```

Project/python_app/Dockerfile

```dockerfile
FROM python:alpine  
WORKDIR /app  
COPY . .  
CMD ["python","main.py"]   
```
!!! ПОНИМАЕТ ТОЛЬКО ДВОЙНЫЕ " '' ["python","main.py"]
## !!!КОНТЕЙНЕР ОСТАНОВИТСЯ ПОЛЕ ОСТАНОВКИ ОСНОВНОГО ПРОЦЕССА УКАЗАННОГО В CMD!!!


```shell
/python_app$ docker build . -t my_calendar
```

```sh
docker images
docker start my_calendar
docker exec -it my_calendar sh
```



----
`/python_app$ docker build . -t my_calendar` создаст репозитроий my_calendar и образ и добавит тег latest
`/python_app$ docker build . -t my_calendar:1.01` если изменить код и создать образ с тегом то можно будет использовать для создания контейнеров и первый образ и второй



`docker logs 479707c8acc8
`

