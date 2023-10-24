```Dockerfile
FROM python:alpine  
ENV PYTHONUNBUFFERED 1  
WORKDIR /app  
COPY requirements.txt /app/  
RUN pip install --no-cache-dir -r requirements.txt  
COPY ./ /app  
CMD ["python", "app.py"]
```

```yaml
version: '3'  
services:  
  web:  
    build: .  
    ports:  
      - "5000:5000"  
    volumes:  
      - .:/app
```

все файлы в одной папке
`docker-compose down --rmi all`

`app.run(host='0.0.0.0',port=5000, debug=True)`: важно проставить IP