GET, POST, PUT, DELETE, и HEAD.

`echo -e curl -X POST http://127.0.0.1:3000/api/belka_api/rrid/8 -H "Content-Type: application/json" -d '{"time": "3000", "value": "2.02"}'`: кодировка


1. GET-запрос:
```bash
curl -X GET https://example.com/api/resource
```

2. POST-запрос с данными в теле (JSON):
```bash
curl -X POST https://example.com/api/resource -H "Content-Type: application/json" -d '{"key1": "value1", "key2": "value2"}'
```

4. POST-запрос с отправкой файла:

```sh
curl -X POST https://example.com/api/upload -F "file=@/path/to/file.jpg"`
```


3. PUT-запрос:
```bash
curl -X PUT https://example.com/api/resource/123 -d "updated_data=NewData"
```

4. DELETE-запрос:
```bash
curl -X DELETE https://example.com/api/resource/123
```

5. HEAD-запрос (запрос только заголовков без тела):
```bash
curl -X HEAD https://example.com/api/resource
```

Это примеры Curl-запросов для всех основных типов HTTP-запросов. Вы можете настраивать заголовки, параметры и данные в соответствии с вашими конкретными потребностями при отправке запросов.