1. CRUD
2. IPYTHON
Консоль django в которую подтягиваются все переменные проекта
```shqll
python manage.py shell
```

CREATE
```python
x = Categories(name='офис')
x.save() 
x.slug = 'ofice'
x.save()

Categories.objects.create(name='Кухня', slug='kuhnya')

```

SELECT
QUERYSET - в документации    
```python
x = Categories.objects.all()
 
In [4]: x
Out[4]: <QuerySet [<Categories: Categories object (1)>, <Categories: Categories object (2)>]>

In [5]: x[0].name
Out[5]: 'Офис'

#Смысл обьекта QuerySet в том что он загружает в себя данные из базы и можно потом использовать их повторно

In [6]:     x.filter(id=1)
Out[6]: <QuerySet [<Categories: Categories object (1)>]>

In [15]: x.filter(id=1)
Out[15]: <QuerySet [<Categories: Categories object (1)>]>

In [20]: z = x.filter(id=2)
In [21]: z
Out[21]: <QuerySet [<Categories: Categories object (2)>]>
In [22]: z[0].name
Out[22]: 'Кухня'


