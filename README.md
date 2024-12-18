# hackaton1_low_mobility_detection

Это проект для хакатона 1 семестра. Идея проекта - оповещать персонал мед клиники о местонахождении маломобильного человека. 


## Как начать работу с нашим проектом?

1. Скачиваем весь проект архивом или клонируем репозиторий, как он есть.

2. Счкачиваем датасет по вот этой ссылке https://universe.roboflow.com/yolotest-vzrks/person-mm3cw/dataset/2
. И извлекаем его в папку datasets.

3. Открываем файл hackaton1_mobility.ipynb - он был сделан как Jupyter Notebook with kernel - Python 3 (ipykernel). На сервисе Google Colab не проверялся, рекомендуется открыть его в Jupyter.
Все необходимые зависимости устанавливаются/импортируются внутри ноутбука. Но ниже приведен список того, что требуется для установки:
   - Torch (pyTorch)
   - ultralytics
   - pytelegrambotapi
   - os
   - PIL
   - telebot

4. И запускаем - готово, вы великолепны! Ну почти великолепны, надо только взять из вывода раздела "Обучаем модель" путь к вашей прекрасной новой модели с наилучшим результатом. Путь указан в таком формате "Logging results to runs\detect\train42". Вместо train42 при каждом запуске обучения будет train с новой цифрой. Именно эту цифру надо найти, и написать ее вместо старой в разделе "Тестируем модель на новых данных".
 
Важное уточнение - в нашем проекте есть бот, его запуск производится из ноутбука (последняя строка), она закомментирована. Перед проверкой бота надо раскомментировать и запустить.


### Датасет
Датасет взят из открытых источников, с сайта https://universe.roboflow.com/
Датасет уже размечен для модели YOLO, в нем 302 фото с людьми на костылях и 101 фото с людьми на инвалидном кресле. Всего 403 фотографии.
В тестовой выборке 49 фото, в выборке для валидации - 76, в тренировочной - 278

### Модель распознавания
Модель распознавания - YOLO 8 версия, модель дообучена на параметрах: 10 эпох, optimizer - SGD (стохастический градиентный спуск).
Дальше идут некоторые параметры модели, на наш взгляд самые интересные: батчи по 16, не сохраняем кэш, эпох - 10, оптимизатор - SGD, скорость обучения - 0.01, параметр momentum - 0.937.
Остальные параметры можно увидеть в ноутбуке. 
Модель дообучается около часа, просим принять это во внимание.

### Отправка сообщений
Для оповещения сделан бот в телеграме, токен закрыт для скачивания, бот очень простой и наивный, зато им легко пользоваться и он может отправлять фото с уведомлением, что обнаружен маломобильный человек.


## Немного о процессе работы

Вся команда работала над проектом, роли отражены в презентации. Идея пришла не быстро, но пришла. 
Мы рассмотрели нескольно вариантов решения, на чек-поинте было сказано, что будет одна модель, в итоге использована другая, описание было выше, а также есть внутри ноутбука. К сожалению, первоначальная модель перегружена сторонними функциями, и нам показалось некорректным брать именно ее, убирать (скорее не использовать) половину ее возможностей, поэтому было принято решение дообучить другую готовую модель.
