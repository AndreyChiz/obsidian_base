
#### Create_table & fill
```python
import psycopg2

# Параметры подключения к базе данных
db_params = {
    'dbname': 'ваша_база_данных',
    'user': 'ваш_пользователь',
    'password': 'ваш_пароль',
    'host': 'ваш_хост',
    'port': 'ваш_порт',
}

# Функция для выполнения SQL-запросов
def execute_sql_query(query):
    try:
        connection = psycopg2.connect(**db_params)
        cursor = connection.cursor()
        cursor.execute(query)
        connection.commit()
        print(f"Запрос успешно выполнен.")
    except (Exception, psycopg2.Error) as error:
        print(f"Ошибка: {error}")
    finally:
        if connection:
            cursor.close()
            connection.close()

# Пример использования
query_create_table = """
    CREATE TABLE IF NOT EXISTS example_table
    (
        id SERIAL PRIMARY KEY,
        name VARCHAR(255),
        age INT
    )
"""

query_insert_data = """
    INSERT INTO example_table (name, age)
    VALUES ('John', 30)
"""

# Выполнение запросов
execute_sql_query(query_create_table)
execute_sql_query(query_insert_data)

```