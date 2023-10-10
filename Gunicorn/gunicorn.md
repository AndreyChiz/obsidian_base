wsgi.py
```python
from app import app # импорт приложения из точки входа flask

if __name__ == "__main__":
    app.run()
```

`gunicorn --bind 0.0.0.0:5000 wsgi:app`: запуск