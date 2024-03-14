```python
from loguru import logger

# Конфигурирование логгера
logger.add("app.log", level="DEBUG", format="{time} {level} {message}", rotation="10 MB")

# Примеры разных уровней логирования
logger.debug("Это сообщение уровня DEBUG")
logger.info("Это сообщение уровня INFO")
logger.warning("Это сообщение уровня WARNING")
logger.error("Это сообщение уровня ERROR")
logger.critical("Это сообщение уровня CRITICAL")
```