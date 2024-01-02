1.
```shell
dajango-admin startproject app #создает главное приложение
python manage.py startapp main #создает приложение
```

2. Добавили созданное приложение.
app.app.settings.py
```python
INSTALLED_APPS = [  
	...
	   
+   "main.apps.MainConfig"  
]
```

3. Добавили функцию обработчик(контроллер)
app.main.views.py
```python
+
def index(request)-> None:  
    return HttpResponse("Home page")

+
def index(request)-> None:
    context: dict = {
        'title': 'home page',
        'content': 'welcome to my magazine',
        'list': ['first', 'second'],
        'dict': {'one': 1},
        'is_autorized': True
    }
    return render(request, 'main/index.html', context)
```

4. Зарегистрировали функцию из п.3  в
app.app.urls.py
```python
urlpatterns = [  
	path('', views.index, name='index'),
    path('about/', views.about, name='about') 
```

5. В папке main.temlates создаем папку с названием соответствующим названию приложения
6. В папке main создаем папку ststic и в ней папку main аналогично п.5 для статики (css, js..)
7. Передали во временный шаблон данные
main.templates.main.index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{ title }}</title>
</head>
<body>
    <p> {{ content }} </p>
	    {% if is_autorized %}
	        <p> {{ list.0 }} </p>
	        <p> {{ dict.one }} </p>
	        <p> {{ bool }} </p>
	    {% endif %}
</body>
</html>
```

8. Заменили тестовый шаблон настоящим. 
9. Подключаем статику - в начале шаблона строка {% load static %}
10. Прокидываем пути статики href="{% static "deps/css/my_css.css" %}"
```html
{% load static %}  
  
<!DOCTYPE html>  
<html lang="en">  
  
<head>  
    <meta charset="UTF-8">  
    <meta http-equiv="X-UA-Compatible" content="IE=edge">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <link rel="stylesheet" href="{% static "deps/css/bootstrap/bootstrap.min.css" %}">  
    <link rel="stylesheet" href="{% static "deps/css/my_css.css" %}">
```