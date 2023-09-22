
```python
class Person:
    """
    Класс для представления человека.

    Attributes:
        name (str): Имя человека.
        age (int): Возраст человека.

    Methods:
        greet(): Представляет человека и приветствует.
        have_birthday(): Увеличивает возраст человека на один год.
    """

    def __init__(self, name, age):
        """
        Инициализация объекта Person.

        Args:
            name (str): Имя человека.
            age (int): Возраст человека.
        """
        self.name = name
        self.age = age

    def greet(self):
        """
        Представляет человека и приветствует.
        """
        print(f"Привет, меня зовут {self.name} и мне {self.age} лет!")

    def have_birthday(self):
        """
        Увеличивает возраст человека на один год.
        """
        self.age += 1

```

