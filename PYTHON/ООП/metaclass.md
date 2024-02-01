Метакласс — это что-то вроде "класса для классов". Он определяет, как должны создаваться классы. Мы можем использовать метаклассы, чтобы автоматически добавлять или изменять поведение классов.

```Python
# Определение метакласса
class SimpleMetaWithArithmeticMethods(type):
    def __new__(cls, name, bases, dct):
        # Метод __new__ вызывается при создании нового класса

        # name: Имя нового класса
        # bases: Кортеж базовых классов
        # dct: Словарь с атрибутами и методами нового класса

        # Простой пример: Добавляем атрибут 'added_attribute' со значением 42
        dct['added_attribute'] = 42

        # Добавляем простые арифметические методы 'add' и 'subtract'
        def add(self, value):
            return self.value + value

        def subtract(self, value):
            return self.value - value

        # Присваиваем методы к классу
        dct['add'] = add
        dct['subtract'] = subtract

        # Вызываем __new__ базового метакласса для создания класса
        return super().__new__(cls, name, bases, dct)

# Использование метакласса для создания класса
class SimpleClassWithArithmeticMethods(metaclass=SimpleMetaWithArithmeticMethods):
    def __init__(self, value):
        # Простой конструктор класса
        self.value = value

# Создание экземпляра класса
simple_instance = SimpleClassWithArithmeticMethods(value=10)

# Вызов арифметических методов
add_result = simple_instance.add(5)
# Результат: 15

subtract_result = simple_instance.subtract(3)
# Результат: 7

```

```python

class MyMeta(type):
    def __new__(cls, name, bases, dct):
        # Изменяем логику метода, добавляя функциональность
        if 'add_numbers' in dct:
            original_method = dct['add_numbers']
            def modified_method(self, a, b, c):
                # Измененная логика метода
                result = original_method(self, a, b) + c
                return result
            dct['add_numbers'] = modified_method

        return super().__new__(cls, name, bases, dct)

class MathOperations(metaclass=MyMeta):
    def add_numbers(self, a, b):
        return a + b

# Создаем экземпляр класса
calculator = MathOperations()

# Используем измененный метод
result = calculator.add_numbers(1, 2, 3)
print(result)  # Вывод: 6

```
