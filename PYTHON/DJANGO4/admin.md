1. Регистрация первого администратора
```shell
python manage.py createsuperuser #Создать админа для админки))
```
2. Отображение таблицы в админ  
goods.admin.py
```python
from django.contrib import admin  
  
  
# 1 Вариант регистрации таблиц для отображения в админ панели  
from goods.models import Categories  
from goods.models import Products  
admin.site.register(Categories)  
admin.site.register(Products)

# 2 Вариант регистрации таблиц для отображения в админ панели 
@admin.register(Categories)  
class CategoriesAdmin(admin.ModelAdmin):  
    prepopulated_fields = {'slug': ('name',)}  #Автоматичеки заполняет поле slug из поля name
    # учитывая тип данных, в данном случае транслитирует строку из поля name в поле slug
  
@admin.register(Products)  
class ProductsAdmin(admin.ModelAdmin):  
    prepopulated_fields = {'slug': ('name',)}
```

3. Изменение языка админ панели
app.settings.py
```python
- LANGUAGE_CODE = 'en-us'
+ LANGUAGE_CODE = 'ru-ru'
```

4. Изменение названий в админ панели
goods.models.py
```python
class Categories(models.Model):  
	name: str = models.CharField(max_length=150,  
	                             ...  
+                                verbose_name='Название' #Для админ панели
	                             )  
	slug: str = models.SlugField(max_length=200,  
								...
+                                verbose_name='URL' #Для админки
	                             )
	...
    class Meta:  
        db_table = 'category'  
+       verbose_name = 'Категорию' #Для единственного числа
+		verbose_name_plural = 'Категории' #для множественного числа

+	def __str__(self):  
+	    return self.name #Отображается в названии обьекта в таблице в админке 

	def __str__(self): # пример использования 
	    return f'{self.name}, количество - {self.quantity}'
```

goods.apps.py
```python
from django.apps import AppConfig  
 
class GoodsConfig(AppConfig):  
    default_auto_field = 'django.db.models.BigAutoField'  
    name = 'goods'  
+    verbose_name = 'Товары' # Название таблицы в админ панели
```