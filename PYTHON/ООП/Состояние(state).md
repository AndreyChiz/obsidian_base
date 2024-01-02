```Python
# Интерфейс состояния для загрузчиков
class DownloaderState:
    def download(self):
        pass

# Конкретные состояния для загрузчиков
class StaticDownloaderState(DownloaderState):
    def download(self):
        return "Static HTML data"

class DynamicDownloaderState(DownloaderState):
    def download(self):
        return "Dynamic HTML data"

# Контекст, который будет использовать различные состояния
class DownloaderContext:
    def __init__(self, state):
        self._state = state

    def set_state(self, state):
        self._state = state

    def download(self):
        return self._state.download()

# Класс, использующий паттерн состояние
class Scrapper:
    def __init__(self, downloader_context, parser):
        self.downloader_context = downloader_context
        self.parser = parser
        self.data = None

    def get_data(self):
        # Вызываем метод download у загрузчика и передаем полученные данные в метод parse у парсера
        html_data = self.downloader_context.download()
        self.data = self.parser.parse(html_data)
        return self.data

# Использование
# Создаем объекты состояний для загрузчиков
static_downloader_state = StaticDownloaderState()
dynamic_downloader_state = DynamicDownloaderState()

# Создаем контексты загрузчиков с начальными состояниями
static_downloader_context = DownloaderContext(static_downloader_state)
dynamic_downloader_context = DownloaderContext(dynamic_downloader_state)

# Создаем объекты парсеров
yodo_parser = YoDoParser()
habr_parser = HabrParser()
fl_parser = FLParser()

# Создаем объекты скрапперов с использованием различных загрузчиков и парсеров
yodo_scrapper = Scrapper(static_downloader_context, yodo_parser)
habr_scrapper = Scrapper(dynamic_downloader_context, habr_parser)
fl_scrapper = Scrapper(static_downloader_context, fl_parser)

# Получаем данные с использованием созданных скрапперов
yodo_data = yodo_scrapper.get_data()
print("YouDo Data:", yodo_data)

habr_data = habr_scrapper.get_data()
print("Habr Data:", habr_data)

fl_data = fl_scrapper.get_data()
print("FL Data:", fl_data)

```