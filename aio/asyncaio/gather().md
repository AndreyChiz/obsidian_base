Синтаксис `asyncio.gather()` выглядит так:
```python
asyncio.gather(*coroutines_or_futures, loop=None, return_exceptions=False)
```



Параметры:
- `*coroutines_or_futures`: Это список асинхронных корутин или объектов `asyncio.Future`, которые нужно запустить параллельно.
- `loop` (необязательный): Этот параметр позволяет указать конкретный цикл событий `asyncio` для выполнения корутин. По умолчанию используется текущий цикл.
- `return_exceptions` (необязательный): Если этот параметр установлен в `True`, то вместо возбуждения исключения при ошибке в корутине, результатом будет список из исключений и значений. По умолчанию `False`.

```python

import asyncio

async def corutine_one(): # 
    print("старт корутины 1")
    await asyncio.sleep(3)
    print("стоп корутины 1")

async def corutine_two():
    print("старт корутины 2")
    await asyncio.sleep(2)
    print('стоп корутны 2')



async def main():
    await asyncio.gather(my_coroutine(), new_foo())

asyncio.run(main())
```

\>
старт корутины 1
старт корутины 2
стоп корутины 2
стоп корутины 1

Функция `main`в данном примере является асинхронной и запускает две корутины `corutine_two()` и `corutine_two` асинхронно с помощью функции `asyncio.gather()`. В результате обе корутины выполняются параллельно в рамках одного потока, что позволяет эффективно использовать асинхронные операции.

----

## Запуск задач из цикла for асинхронно


```python

import asyncio

async def my_coroutine(number):
    print(f"Coroutine {number} started")
    await asyncio.sleep(number)
    print(f"Coroutine {number} finished")

async def main():
    tasks = []
    for i in range(1, 4):
        task = asyncio.create_task(my_coroutine(i))
        tasks.append(task)

    await asyncio.gather(*tasks)

asyncio.run(main())
```
В этом примере мы создаем асинхронные задачи в цикле `for` с помощью `asyncio.create_task()` и добавляем их в список `tasks`. Затем мы используем `asyncio.gather()` с оператором `*` перед `tasks`, чтобы ожидать выполнения всех задач параллельно. Это позволяет создать и запустить несколько задач в цикле и эффективно дождаться их завершения.


----

## Обработка ошибок
```python
import asyncio

async def func1():
    await asyncio.sleep(2)
    return "Result from func1"

async def func2():
    await asyncio.sleep(1)
    raise ValueError("An error occurred in func2")

async def main():
    try:
        results = await asyncio.gather(func1(), func2(), return_exceptions=True)
        print("Results:", results)
    except ValueError as e:
        print("Caught an exception:", e)

asyncio.run(main())
```

В этом примере `return_exceptions` установлен в `True`, поэтому при возникновении исключения в `func2()`, результатом `asyncio.gather()` будет список из значений и исключений.

----
## Запуск в другом потоке

```python
import asyncio
import threading

async def my_coroutine():
    print("Coroutine started")
    await asyncio.sleep(2)
    print("Coroutine finished")
    return "Coroutine result"

def run_async_in_thread():
    loop = asyncio.new_event_loop()
    asyncio.set_event_loop(loop)
    
    future = asyncio.run_coroutine_threadsafe(my_coroutine(), loop)
    result = future.result()

    print("Result in thread:", result)

    loop.close()

# Запуск асинхронной функции в другом потоке
thread = threading.Thread(target=run_async_in_thread)
thread.start()
thread.join()

```
В этом примере создается новый поток с помощью модуля `threading`, и в этом потоке вызывается функция `run_async_in_thread()`, которая создает новый асинхронный цикл, использует `asyncio.run_coroutine_threadsafe()` для запуска асинхронной функции `my_coroutine()`.