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
app.main.views.py и передали в шаблон переменную context
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

name='index' можно применять index как ссылку в html разметке
```html
<a class="navbar-brand" href= "{% url 'main:index' %}">Home</a>
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
...
	<link rel="stylesheet" href="{% static "deps/css/my_footer_css.css" %}">
...
<title>{{ title }}</title>
```

11. Заменили путь к статике добавив в app.settings.py строку STATICFILES_DIRS в которой BASE_DIR - путь (уровень папки проекта) чтобы статика искалась в этой папке, переместили папку static в корень проекта.
```python
STATIC_URL = 'static/'  #это префикс в пути к статие отображаемый в браузере
  
+ STATICFILES_DIRS = [  
    BASE_DIR / 'static'  
]

```

12. Создаем в папке main.templates.main файл base.html в который помещаем все повторяющиеся теги из index.html. Это будет базовый шаблон который будем расширять.
13. Пример вынесения блока из базового шаблона main.templates.main.base.html
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
...
-	<link rel="stylesheet" href="{% static "deps/css/my_footer_css.css" %}">
+   {% block footer_css %}{% endblock %} 
...
<title>{{ title }}</title>
...
<div class="col-lg-10">  
    <!-- Контент на странице выносим в index.html -->  
+    {% block content %} {% endblock %}  
</div>
```

14. main.templates.main.index.html
	строка	{% extends "main/base.html" %} указывает откуда будет добавляться код
	строка {% block footer_css %} блок который будет добавляться в код при вызове данного шаблона
	Переменную context которую мы передали через функцию из п.3 можно использовать в файле который расширяем(index.html) и в файле которым расширяем(base.html).
	то-есть контекстные переменные переданные через функцию в views.py НЕЯВНО! наследуются в расширяемые и расширяющиеся шаблоны.
```html
{% extends "main/base.html" %}  
{% load static %}  
  
  
{% block footer_css %}  
    <link rel="stylesheet" href="{% static "deps/css/my_footer_css.css" %}">  
{% endblock %}

{% block content %}  
    <!-- Контент на странице -->  
    <h1 class="mt-5 pt-5"><strong>{{ content }}</strong></h1>  
{% endblock %}
```

15. Пример расширения 
main.views.py
```python
+
def about(request)-> None:  
    context: dict = {  
        'title': 'About - О Нас',  
        'content': 'О нас',  
        'text_on_page': 'Описание магазина'  
    }  
    return render(request, 'main/about.html', context)
```

main.templates.main.about.html
```html
{% extends "main/base.html" %}  
{% load static %}  
  
  
{% block footer_css %}  
    <link rel="stylesheet" href="{% static "deps/css/my_footer_css.css" %}">  
{% endblock %}  
  
  
{% block content %}  
    <!-- Контент на странице -->  
    <div class="mt-5 pt-5 bg-white custom-shadow rounded">  
        <h3 class="m-2"> {{ content }} </h3>  
        <p class="m-2" >{{ text_on_page }}</p>  
    </div>{% endblock %}
```

16. Привязка URL в основном приложении
Создаем в приложении main свой файл urls.py
 main.urls.py
```python
from django.urls import path  
from main import views  #Не забудь!!!
  
app_name = 'main'  #переменная для указания области видимости в параметре namespace в app.url.py
  
urlpatterns = [  
    path('', views.index, name='index'),  
    path('about/', views.about, name='about')  
]
```

app.url.py
```python
from django.contrib import admin  
from django.urls import path, include  
  
  
urlpatterns = [  
    path('admin/', admin.site.urls),  
    path('', include('main.urls', namespace='main')),  
    path('catalog/', include('goods.urls', namespace='catalog'))  
  
]
```
namespace нужно для того чтобы ссылки из параметра name (п.16 main.urls.py urlspattern) используемые в разметке привязывались корректно, т.к. якоря index и adbout могут повторяться в других модулях.
было:
```html
<a class="navbar-brand" href= "{% url 'index' %}">Home</a>
<li><a class="dropdown-item  text-white" href="{% url 'about' %}">Про нас</a></li>
```
стало: 
```html
<a class="navbar-brand" href= "{% url 'main:index' %}">Home</a>
<li><a class="dropdown-item  text-white" href="{% url 'main:about' %}">Про нас</a></li>
```

17. Работа с For в шаблоне
```html
{% for product in goods %}  
    <!-- Карта товара -->  
    <div class="col-lg-4 col-md-6 p-4">  
        <div class="card border-primary rounded custom-shadow">  
            <img src={% static product.image %} class="card-img-top" alt="...">  
            <div class="card-body">  
                <a href="product.html">  
                    <p class="card-title">{{ product.name }}</p>  
                </a>                
	                <p class="card-text text-truncate">{{ product.description }}</p>  
	                <p class="product_id">id: 02265</p>  
					<p><strong>{{ product.price }} $</strong></p>  
				<a href="#" class="btn add-to-cart">  
					<img class="mx-1" src="{% static "deps/icons/cart-plus.svg" %}" alt="Catalog Icon"  width="32" height="32">  
                </a>                
            </div>            
        </div>        
    </div>
{% endfor %}
```