1. **Хранение значений полей:** Значения полей `namedtuple` хранятся внутри экземпляра объекта. Они хранятся плотно в памяти, как элементы кортежа.
    
2. **Доступ к значениям полей:** При обращении к значению поля через атрибут (например, `person.name`), интерпретатор Python проверяет атрибут `name` в словаре `person.__dict__`. Если он не находит его там, он ищет его в атрибутах класса `Person` и его родителей.
    
3. **Кеширование и повторное использование:** Имена полей и структура класса кешируются в памяти, что делает экземпляры `namedtuple` легковесными. Если вы создадите множество экземпляров `namedtuple` с одинаковыми именами полей и структурой класса, то они будут использовать одну и ту же структуру класса в памяти.


```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'gender'])

# Создаем несколько объектов Person
person1 = Person(name='Alice', age=30, gender='female')
person2 = Person(name='Bob', age=25, gender='male')
person3 = Person(name='Charlie', age=35, gender='male')

# Сохраняем объекты в списке
people = [person1, person2, person3]

# Выводим информацию о каждом объекте в списке
for person in people:
    print(person.name, person.age, person.gender)
```