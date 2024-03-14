
```Python
# Продукт
class Scrapper:
    def __init__(self):
        self.downloader = None
        self.parser = None
        self.data = None

    def get_data(self):
        if self.downloader and self.parser:
            # Вызываем метод download у загрузчика и передаем полученные данные в метод parse у парсера
            html_data = self.downloader.download()
            self.data = self.parser.parse(html_data)
            return self.data
        else:
            return None

# Интерфейс строителя
class ScrapperBuilder:
    def build_downloader(self):
        pass
    
    def build_parser(self):
        pass
    
    def get_scrapper(self):
        pass

# Загрузчики
class StaticDownloader:
    def download(self):
        # В реальном коде здесь будет логика загрузки HTML данных
        return "Static HTML data"

class DynamicDownloader:
    def download(self):
        # В реальном коде здесь будет логика динамической загрузки HTML данных
        return "Dynamic HTML data"

# Парсеры

class YoDoParser:
    def parse(self, data):
        # В реальном коде здесь будет логика парсинга данных для YouDo
        return "Parsed data from YouDo Parser"

class HabrParser:
    def parse(self, data):
        # В реальном коде здесь будет логика парсинга данных для Habr
        return "Parsed data from Habr Parser"

class FLParser:
    def parse(self, data):
        # В реальном коде здесь будет логика парсинга данных для FL
        return "Parsed data from FL Parser"

# Конкретный строитель для YouDoScrapper
class YouDoScrapperBuilder(ScrapperBuilder):
    def __init__(self):
        self.scrapper = Scrapper()

    def build_downloader(self):
        self.scrapper.downloader = DynamicDownloader()

    def build_parser(self):
        self.scrapper.parser = YoDoParser()

    def get_scrapper(self):
        return self.scrapper

# Конкретный строитель для HabrScrapper
class HabrScrapperBuilder(ScrapperBuilder):
    def __init__(self):
        self.scrapper = Scrapper()

    def build_downloader(self):
        self.scrapper.downloader = StaticDownloader()

    def build_parser(self):
        self.scrapper.parser = HabrParser()

    def get_scrapper(self):
        return self.scrapper

# Конкретный строитель для FLScrapper
class FLScrapperBuilder(ScrapperBuilder):
    def __init__(self):
        self.scrapper = Scrapper()

    def build_downloader(self):
        self.scrapper.downloader = StaticDownloader()

    def build_parser(self):
        self.scrapper.parser = FLParser()

    def get_scrapper(self):
        return self.scrapper

# Директор (опционально, можно не использовать)
class ScrapperDirector:
    def __init__(self, builder):
        self.builder = builder

    def construct_scrapper(self):
        self.builder.build_downloader()
        self.builder.build_parser()

# Использование
youdo_builder = YouDoScrapperBuilder()
habr_builder = HabrScrapperBuilder()
fl_builder = FLScrapperBuilder()

youdo_builder.construct_scrapper()
habr_builder.construct_scrapper()
fl_builder.construct_scrapper()

youdo_scrapper = youdo_builder.get_scrapper()
habr_scrapper = habr_builder.get_scrapper()
fl_scrapper = fl_builder.get_scrapper()

# Теперь у нас есть три скраппера с различными загрузчиками и парсерами
# Вызываем метод get_data для получения данных после загрузки и парсинга
youdo_data = youdo_scrapper.get_data()
habr_data = habr_scrapper.get_data()
fl_data = fl_scrapper.get_data()

print("YouDo Data:", youdo_data)
print("Habr Data:", habr_data)
print("FL Data:", fl_data)


```