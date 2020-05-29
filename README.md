# <a name="up" />Портфолио

[Проектирование тестов](#test-design)

[Тестирование веб-приложений](#web-testing)

[Тестирование мобильных приложений](#mobile-testing)

[Тестирование API](#api-testing)

[Основы баз данных](#data-bases)

[Основы автоматизации тестирования](#test-automation)

## <a name="test-design" />Проектирование тестов

### Задание

### Решение

[Наверх](#up)

## <a name="web-testing" />Тестирование веб-приложений

### Задание

### Решение

[Наверх](#up)

## <a name="mobile-testing" />Тестирование мобильных приложений

### Задание

1. Проанализируй требования к мобильному приложению Яндекс.Метро.
2. Напиши чек-лист для тестирования мобильного приложения на часть требований, **выделенных жирным шрифтом**.
3. Протестируй мобильное приложение в эмуляторе с помощью Android Studio или на своём Android-устройстве и заведи баг-репорты. Скачай готовящуюся к релизу версию приложения тут.

    Чтобы проверить, что обновление происходит корректно, скачай предыдущую версию тут.

4. Напиши отчет о тестировании. Что можешь рассказать команде о статусе протестированной части продукта?

### Решение

[Наверх](#up)

## <a name="api-testing" />Тестирование API

### Задание

1. Проанализируй требования к API бэкенда Яндекс.Метро.

<details><summary>Требования к API Метро</summary>

Метро использует API "metrokit-service". Это API для библиотеки MetroKit.

Функциональность metrokit-service включает:

- Доступ к полному списку схем — GET /v1/list/
- Доступ к cписку актуальных событий для выбранной схемы — GET /v1/events/

**GET /v1/list/**

GET на URI: https://metrokit-service.maps.yandex.net/v1/list

Ответ — полный список схем по всем городам. Ответ всегда в формате JSON.

Пример структуры ответа Москвы.

```bash
        {
            "id": "sc34974011",
            "name": {
                "en": "Moscow",
                "ru": "Москва",
                "tr": "Moskova",
                "uk": "Москва"
            },
            "size": {
                "packed": 369292,
                "unpacked": 3001856
            },
            "tags": [
                "published"
            ],
            "aliases": [
                "moscow"
            ],
            "logoUrl": "https://avatars.mds.yandex.net/get-bunker/128809/6f088274a46aee3df308423d222eb36906825cb7/orig",
            "version": "2e5e649",
            "geoRegion": {
                "delta": {
                    "lat": 0.32158,
                    "lon": 0.439453
                },
                "center": {
                    "lat": 55.743347,
                    "lon": 37.617188
                }
            },
            "countryCode": "RU",
            "defaultAlias": "moscow"
        }
```

**GET /v1/events/**

GET на URI: https://metrokit-service.maps.yandex.net/v1/events

Параметр: scheme_id=\<id>

Пример: https://metrokit-service.maps.yandex.net/v1/events?scheme_id=sc34974011

Ответ — список событий для выбранной схемы. Ответ всегда в формате JSON.

Если событие присутствует, ответ имеет такую структуру. Например, для Москвы с id = sc34974011:

```bash
    "events": {
        "type": "IndexedCollection",
        "items": [
            {
                "id": "ev-76c50f2d-9c3d-4835-ac73-a0544b1b308e",
                "schedule": {
                    "to": "2019-10-25T23:10:00+03:00",
                    "from": "2019-03-30T01:00:00+03:00",
                    "type": "Interval"
                },
                "title": {
                    "en": "No trains to Kakhovskaya station",
                    "ru": "Поезда не ходят до «Каховской»"
                },
                "description": {
                    "en": "Station closure",
                    "ru": "Закрытие станции"
                },
                "changeIds": [
                    "ch-feed3c7d-d35e-4481-87a4-7c141e1c96c0"
                ]
            }
  }
```

Если события отсутствуют, список может быть пустым, но должен возвращаться в формате JSON. Например, для Хельсинки с id = sc38955480:

```bash
{
    "events": {
        "type": "IndexedCollection",
        "items": []
    },
    "changes": {
        "type": "IndexedCollection",
        "items": []
    }
}
```

</details>

2. Протестируй API бэкенда Яндекс.Метро:

	2.1. по чек-листу из шаблона;

    <details>
    <summary>2.2. по инструкции.</summary>

    Инструкция для тестирования API
    - Зайди в postman.
    - Получи список схем из запроса «/list».
    - Составь таблицу в третьей вкладке шаблона, сопоставив каждому городу его id.
    - Дополни чек-лист для запроса «/events». Убедись, что для каждого id возвращается ответ согласно требованиям.
    - Проверь корректность работы запроса «/events».

    </details>

    В процессе тестирования отмечай результаты выполнения теста: PASSED или FAILED. Если тест со статусом FAILED, заведи баг-репорт в Яндекс.Трекере в очереди BUG и вписывай ID в соответствующую таблицу результатов.

3. Напиши отчет о тестировании. Что можешь рассказать команде о статусе протестированной части продукта?

### Решение

1. Данные схем

| Город  | ID схемы  |
|:----------|:----------|
|Новосибирск    | sc02877545    |
|Москва	    | sc34974011    |
|Киев	    | sc21078879    |
|Сан-Франциско	    | sc99912    |
|Алматы	    | sc37730841    |
|Хельсинки	    | sc38955480    |
|Лиссабон	    | sc39559734    |
|Днепр	    | sc47063979    |
|Дубай	    | sc19930717    |
|Бухарест	    | sc66937172    |
|Афины	    | sc92836217    |
|София	    | sc29665623    |
|Казань	    | sc63288776    |
|Минск	    | sc31709615    |
|Вена	    | sc52507030    |
|Харьков	    | sc12039691    |
|Милан	    | sc999    |
|Будапешт	    | sc04704892    |
|Ташкент	    | sc19351236    |
|Тбилиси	    | sc46903964    |
|Варшава	    | sc12943371    |
|Волгоград	    | sc03517743    |
|Санкт-Петербург	    | sc60983525    |
|Ереван	    | sc95957238    |
|Прага	    | sc20559874    |
|Екатеринбург	    | sc58473698    |
|Баку	    | sc54283234    |
|Самара	    | sc33333931    |
|Стамбул	    | sc97451070    |
|Нижний Новгород	    | sc77792237    |
|Рим	    | sc68078330    |

[Наверх](#up)

## <a name="data-bases" />Основы баз данных (PostgreSQL)

### Задание 1

От разработчиков поступила задача: нужно выяснить, какие запросы шли на IP-адреса. IP-адрес состоит из четырёх чисел, они разделены точками. Тебе нужны адреса, которые начинаются с "233.201.".

Логи лежат на удалённом сервере по адресу logs/2019/12. День, когда случилась ошибка, неизвестен.

Твоя задача — узнать, какие запросы были отправлены.

В ответе приложи:
1. Команду, которой тебе удалось получить нужные логи.
2. Подходящие строки, например:

```bash
184.79.247.161 - - [30/12/2019:21:38:13 +0000] "PUT /alerts HTTP/1.1" 400 3557
```

### Решение

1. Команда получения логов:

```bash
grep ^233.201 /logs/2019/12/*.txt
```

2. Логи:

```bash
233.201.188.154 - - [18/12/2019:21:46:01 +0000] "DELETE /events HTTP/1.1" 403 3971
233.201.182.9 - - [21/12/2019:21:56:20 +0000] "PATCH /users HTTP/1.1" 400 4118
```

[Наверх](#up)

### Задание 2

В системе обнаружен баг. Он проявлялся 30.12.2019 и 31.12.2019 с 21:30:00 до 21:39:59. При этом появлялись ошибки с номерами 400 и 500. Твоя задача — сохранить в отдельный файл логи, которые были записаны в этот период. Затем эти логи надо разложить по отдельным файлам: логи с одинаковой ошибкой положи в один файл.

Как это сделать:
1. В домашней директории на удалённом сервере создай директорию bug1.
2. Все запросы, которые произошли в указанный период, положи в файл main.txt.
3. Внутри директории bug1 создай директорию events.
4. Внутри директории events создай файлы для ошибок с номерами 400 и 500. Назови эти файлы 400.txt и 500.txt соответственно. В них выдели логи с соответствующей ошибкой из файла main.txt.

В ответе приложи:
1. Команды, которые создают директории bug1 и events.
2. Команду, которой ты выбираешь запросы за указанный период. Это те запросы, которыми ты отбираешь логи в файл main.txt.
3. Команды, которыми ты кладёшь логи в файлы 400.txt и 500.txt из main.txt.
4. Тексты файлов 400.txt и 500.txt.

#### Описание базы данных

База данных о поездках такси в Чикаго:

Таблица `neighborhoods` — информация о районах города:
- `neighborhood_id` — код района;
- `name` — название района.
Таблица `cabs` — информация о такси:
- `cab_id` — код автомобиля;
- `vehicle_id` — технический идентификатор автомобиля;
- `company_name` — компания, которой принадлежит автомобиль.
Таблица `trips` — информация о поездках:
- `trip_id` — код поездки;
- `cab_id` — код автомобиля, на котором была совершена поездка;
- `start_ts` — дата и время начала поездки (время округлено до часа);
- `end_ts` — дата и время окончания поездки (время округлено до часа);
- `duration_seconds` — длительность поездки в секундах;
- `distance_miles` — дальность поездки в милях;
- `pickup_location_id` — код района города, в котором была начата поездка;
- `dropoff_location_id` — код района города, в котором завершилась поездка.
Таблица `weather_records` — информация о погоде:
- `record_id` — код записи погодных наблюдений;
- `ts` — дата и время наблюдения (время округлено до часа);
- `temperature` — температура на момент наблюдения;
- `description` — краткое описание погодных условий. Например, 'light rain' или 'scattered clouds'.

#### Схема таблиц

![Схема таблиц БД](https://code.s3.yandex.net/qa/schemes/project_4_sprint.png)

В базе данных нет прямой связи между таблицами `trips` и `weather_records`. Связать эти таблицы можно по времени начала поездки (`trips.start_ts`) и моменту погодных наблюдений (`weather_records.ts`).

### Решение

1. Команды создания директорий bug1 и events:

```bash
mkdir bug1
mkdir events
```

2. Команда выбора запросов за указанный период:

```bash
grep "21:3" ~/logs/2019/12/apache_2019-12-30.txt > ~/bug1/main.txt
grep "21:3" ~/logs/2019/12/apache_2019-12-31.txt >> ~/bug1/main.txt
```

3. Команды сохранения логов в файлы 400.txt и 500.txt из main.txt:

```bash
grep -w "400" ~/bug1/main.txt > ~/bug1/events/400.txt
grep -w "500" ~/bug1/main.txt > ~/bug1/events/500.txt
```

<details>
<summary>4. 400.txt</summary>

```bash
80.57.170.51 - - [30/12/2019:21:35:12 +0000] "DELETE /users HTTP/1.1" 400 3623
204.235.176.118 - - [30/12/2019:21:35:13 +0000] "POST /users HTTP/1.1" 400 4704
82.95.203.67 - - [30/12/2019:21:35:19 +0000] "DELETE /lists HTTP/1.1" 400 3737
155.242.215.46 - - [30/12/2019:21:35:38 +0000] "POST /playbooks HTTP/1.1" 400 4450
189.176.85.0 - - [30/12/2019:21:35:39 +0000] "PATCH /alerts HTTP/1.1" 400 2732
13.108.71.71 - - [30/12/2019:21:35:43 +0000] "PATCH /events HTTP/1.1" 400 3410
195.213.133.182 - - [30/12/2019:21:35:46 +0000] "PUT /customers HTTP/1.1" 400 3085
235.243.133.78 - - [30/12/2019:21:35:47 +0000] "PATCH /customers HTTP/1.1" 400 3264
192.57.115.49 - - [30/12/2019:21:35:55 +0000] "POST /parsers HTTP/1.1" 400 2457
71.0.49.244 - - [30/12/2019:21:35:55 +0000] "PUT /collectors HTTP/1.1" 400 2785
224.159.206.126 - - [30/12/2019:21:36:02 +0000] "DELETE /customers HTTP/1.1" 400 4569
131.35.106.246 - - [30/12/2019:21:36:04 +0000] "DELETE /lists HTTP/1.1" 400 2578
216.24.42.208 - - [30/12/2019:21:36:06 +0000] "GET /parsers HTTP/1.1" 400 4597
123.53.150.160 - - [30/12/2019:21:37:19 +0000] "PATCH /events HTTP/1.1" 400 4379
61.129.127.103 - - [30/12/2019:21:37:32 +0000] "GET /lists HTTP/1.1" 400 2575
90.216.4.78 - - [30/12/2019:21:37:34 +0000] "PATCH /lists HTTP/1.1" 400 3899
204.250.214.208 - - [30/12/2019:21:37:36 +0000] "PATCH /parsers HTTP/1.1" 400 4742
79.214.240.98 - - [30/12/2019:21:37:37 +0000] "POST /fieldsets HTTP/1.1" 400 4441
65.47.42.12 - - [30/12/2019:21:37:39 +0000] "PATCH /customers HTTP/1.1" 400 2500
251.118.141.34 - - [30/12/2019:21:37:41 +0000] "POST /customers HTTP/1.1" 400 3519
205.20.166.196 - - [30/12/2019:21:37:51 +0000] "POST /users HTTP/1.1" 400 4032
156.217.3.46 - - [30/12/2019:21:37:52 +0000] "PATCH /parsers HTTP/1.1" 400 2020
48.240.198.167 - - [30/12/2019:21:37:57 +0000] "PATCH /playbooks HTTP/1.1" 400 4100
101.255.159.211 - - [30/12/2019:21:37:59 +0000] "GET /auth HTTP/1.1" 400 2324
80.76.98.203 - - [30/12/2019:21:38:00 +0000] "POST /playbooks HTTP/1.1" 400 3045
85.64.63.255 - - [30/12/2019:21:38:13 +0000] "PATCH /collectors HTTP/1.1" 400 2291
184.79.247.161 - - [30/12/2019:21:38:13 +0000] "PUT /alerts HTTP/1.1" 400 3557
93.2.134.22 - - [30/12/2019:21:39:39 +0000] "DELETE /alerts HTTP/1.1" 400 3701
86.34.86.182 - - [31/12/2019:21:35:10 +0000] "POST /auth HTTP/1.1" 400 3626
167.37.16.117 - - [31/12/2019:21:35:17 +0000] "PATCH /customers HTTP/1.1" 400 3294
199.128.92.19 - - [31/12/2019:21:35:43 +0000] "PUT /users HTTP/1.1" 400 4180
162.152.99.143 - - [31/12/2019:21:35:59 +0000] "PUT /users HTTP/1.1" 400 4606
83.115.59.224 - - [31/12/2019:21:37:26 +0000] "GET /alerts HTTP/1.1" 400 3489
194.10.97.226 - - [31/12/2019:21:37:31 +0000] "DELETE /lists HTTP/1.1" 400 2447
180.99.214.40 - - [31/12/2019:21:37:44 +0000] "DELETE /alerts HTTP/1.1" 400 2077
154.152.205.4 - - [31/12/2019:21:37:50 +0000] "GET /playbooks HTTP/1.1" 400 3324
197.82.125.54 - - [31/12/2019:21:37:52 +0000] "PUT /fieldsets HTTP/1.1" 400 4365
115.89.87.219 - - [31/12/2019:21:38:06 +0000] "PUT /playbooks HTTP/1.1" 400 2589
100.77.15.14 - - [31/12/2019:21:38:07 +0000] "GET /fieldsets HTTP/1.1" 400 4911
22.33.159.242 - - [31/12/2019:21:38:07 +0000] "GET /playbooks HTTP/1.1" 400 3955
149.148.229.11 - - [31/12/2019:21:39:16 +0000] "GET /users HTTP/1.1" 400 2071
236.107.64.192 - - [31/12/2019:21:39:17 +0000] "PATCH /users HTTP/1.1" 400 2791
24.156.105.39 - - [31/12/2019:21:39:23 +0000] "GET /lists HTTP/1.1" 400 2902
193.50.164.254 - - [31/12/2019:21:39:23 +0000] "PUT /playbooks HTTP/1.1" 400 3296
18.123.104.91 - - [31/12/2019:21:39:52 +0000] "GET /collectors HTTP/1.1" 400 4372
234.218.148.4 - - [31/12/2019:21:39:54 +0000] "PUT /users HTTP/1.1" 400 2509
```

</details>

<details>
<summary>5. 500.txt</summary>

```bash
64.250.112.189 - - [30/12/2019:21:35:13 +0000] "PUT /parsers HTTP/1.1" 500 4639
193.253.101.180 - - [30/12/2019:21:35:31 +0000] "PATCH /alerts HTTP/1.1" 500 2944
197.106.117.194 - - [30/12/2019:21:35:31 +0000] "PATCH /parsers HTTP/1.1" 500 3519
247.124.71.67 - - [30/12/2019:21:35:45 +0000] "PUT /alerts HTTP/1.1" 500 2746
62.88.204.119 - - [30/12/2019:21:35:51 +0000] "PUT /auth HTTP/1.1" 500 2666
125.156.142.26 - - [30/12/2019:21:36:01 +0000] "PATCH /events HTTP/1.1" 500 3460
144.170.212.70 - - [30/12/2019:21:36:04 +0000] "DELETE /parsers HTTP/1.1" 500 2599
59.39.200.252 - - [30/12/2019:21:36:05 +0000] "GET /alerts HTTP/1.1" 500 2650
150.136.200.100 - - [30/12/2019:21:37:24 +0000] "POST /lists HTTP/1.1" 500 2684
84.81.25.45 - - [30/12/2019:21:37:25 +0000] "POST /auth HTTP/1.1" 500 2052
30.222.160.141 - - [30/12/2019:21:37:30 +0000] "PATCH /parsers HTTP/1.1" 500 2017
117.87.158.36 - - [30/12/2019:21:37:34 +0000] "POST /fieldsets HTTP/1.1" 500 4056
212.153.128.212 - - [30/12/2019:21:37:42 +0000] "PUT /fieldsets HTTP/1.1" 500 3259
58.188.83.217 - - [30/12/2019:21:37:46 +0000] "POST /playbooks HTTP/1.1" 500 3947
193.123.131.146 - - [30/12/2019:21:37:47 +0000] "PUT /lists HTTP/1.1" 500 3902
182.7.179.91 - - [30/12/2019:21:37:48 +0000] "GET /users HTTP/1.1" 500 2950
10.25.168.164 - - [30/12/2019:21:38:05 +0000] "PATCH /playbooks HTTP/1.1" 500 3858
215.201.210.173 - - [30/12/2019:21:38:11 +0000] "PATCH /customers HTTP/1.1" 500 3277
179.241.103.167 - - [30/12/2019:21:39:23 +0000] "POST /lists HTTP/1.1" 500 3669
147.188.170.252 - - [30/12/2019:21:39:33 +0000] "POST /fieldsets HTTP/1.1" 500 3313
1.249.123.189 - - [30/12/2019:21:39:36 +0000] "PATCH /alerts HTTP/1.1" 500 4734
124.114.135.105 - - [30/12/2019:21:39:41 +0000] "PATCH /customers HTTP/1.1" 500 3348
35.215.100.202 - - [30/12/2019:21:39:43 +0000] "PUT /alerts HTTP/1.1" 500 4345
86.222.23.128 - - [30/12/2019:21:39:44 +0000] "PATCH /alerts HTTP/1.1" 500 2230
20.161.75.95 - - [30/12/2019:21:39:48 +0000] "DELETE /users HTTP/1.1" 500 2412
196.18.151.117 - - [30/12/2019:21:39:55 +0000] "PUT /events HTTP/1.1" 500 4439
77.101.138.151 - - [30/12/2019:21:39:57 +0000] "PUT /lists HTTP/1.1" 500 2194
208.205.133.127 - - [31/12/2019:21:35:17 +0000] "DELETE /alerts HTTP/1.1" 500 4561
20.145.255.91 - - [31/12/2019:21:35:30 +0000] "GET /parsers HTTP/1.1" 500 3051
91.66.134.13 - - [31/12/2019:21:35:53 +0000] "POST /lists HTTP/1.1" 500 3319
31.88.211.206 - - [31/12/2019:21:35:57 +0000] "DELETE /events HTTP/1.1" 500 2325
171.37.114.114 - - [31/12/2019:21:37:39 +0000] "DELETE /fieldsets HTTP/1.1" 500 3253
223.157.242.167 - - [31/12/2019:21:37:59 +0000] "POST /users HTTP/1.1" 500 2283
98.181.102.34 - - [31/12/2019:21:38:06 +0000] "PATCH /fieldsets HTTP/1.1" 500 4672
254.74.22.79 - - [31/12/2019:21:38:06 +0000] "PUT /lists HTTP/1.1" 500 2259
103.46.238.3 - - [31/12/2019:21:38:09 +0000] "PUT /lists HTTP/1.1" 500 3992
41.62.205.107 - - [31/12/2019:21:39:20 +0000] "PATCH /alerts HTTP/1.1" 500 3631
22.53.105.197 - - [31/12/2019:21:39:31 +0000] "DELETE /collectors HTTP/1.1" 500 4202
178.22.133.42 - - [31/12/2019:21:39:43 +0000] "PUT /alerts HTTP/1.1" 500 4648
102.247.13.50 - - [31/12/2019:21:39:55 +0000] "PATCH /auth HTTP/1.1" 500 3736
171.37.114.114 - - [31/12/2019:21:37:39 +0000] "DELETE /fieldsets HTTP/1.1" 500 3253
223.157.242.167 - - [31/12/2019:21:37:59 +0000] "POST /users HTTP/1.1" 500 2283
98.181.102.34 - - [31/12/2019:21:38:06 +0000] "PATCH /fieldsets HTTP/1.1" 500 4672
254.74.22.79 - - [31/12/2019:21:38:06 +0000] "PUT /lists HTTP/1.1" 500 2259
103.46.238.3 - - [31/12/2019:21:38:09 +0000] "PUT /lists HTTP/1.1" 500 3992
41.62.205.107 - - [31/12/2019:21:39:20 +0000] "PATCH /alerts HTTP/1.1" 500 3631
22.53.105.197 - - [31/12/2019:21:39:31 +0000] "DELETE /collectors HTTP/1.1" 500 4202
178.22.133.42 - - [31/12/2019:21:39:43 +0000] "PUT /alerts HTTP/1.1" 500 4648
102.247.13.50 - - [31/12/2019:21:39:55 +0000] "PATCH /auth HTTP/1.1" 500 3736
```

</details>

[Наверх](#up)

### Задание 3

У тебя есть база данных с поездками на такси. По плану на линию обслуживания должно было выйти 10550 автомобилей — эта цифра покрывает спрос пользователей. Команде поступило много жалоб — свободных автомобилей оказалось недостаточно. Сколько такси вышло на линии на самом деле? Информация о всех машинах на линии есть в таблице `cabs`.
1. Зайди на удалённый сервер.
2. Подключись к базе данных `chicago_taxi`.
3. Посчитай, сколько всего автомобилей в таблице `cabs`.

В ответе приложи:
1. Число автомобилей
2. Запрос, которым тебе удалось решить задачу.

### Решение

1. Число автомобилей: 5529.
2. Запрос:

```bash
SELECT
  COUNT(*) AS cnt
FROM cabs;
```

[Наверх](#up)

### Задание 4

Посчитай количество автомобилей в каждой компании из таблицы `cabs`. Отсортируй значения по убыванию. Команда предполагает, что некоторые компании не вывели достаточно автомобилей на линию.

Выведи те компании, в которых меньше 100 автомобилей. Поле с числом автомобилей назови `cnt`, поле с названием компании — `company_name`.

Чтобы решить задачу, примени оператор HAVING — аналог WHERE для агрегирующих функций.

В ответе приложи:
1. Список компаний с числом автомобилей меньше 100.
2. Запрос, которым тебе удалось решить задачу.

### Решение

<details>

<summary>1. Список компаний с числом автомобилей меньше 100.</summary>

```bash
                 company_name                 | cnt 
----------------------------------------------+-----
 Nova Taxi Affiliation Llc                    |  97
 Patriot Taxi Dba Peace Taxi Associat         |  89
 Blue Diamond                                 |  85
 Checker Taxi Affiliation                     |  81
 Chicago Medallion Management                 |  80
 Chicago Independents                         |  69
 24 Seven Taxi                                |  67
 Checker Taxi                                 |  60
 American United                              |  55
 Chicago Medallion Leasing INC                |  53
 Top Cab Affiliation                          |  49
 KOAM Taxi Association                        |  48
 Chicago Taxicab                              |  38
 Norshore Cab                                 |  34
 Gold Coast Taxi                              |  20
 Metro Group                                  |  20
 Service Taxi Association                     |  18
 5 Star Taxi                                  |  14
 American United Taxi Affiliation             |   8
 Metro Jet Taxi A                             |   8
 Setare Inc                                   |   7
 Leonard Cab Co                               |   5
 4615 - 83503 Tyrone Henderson                |   1
 5062 - 34841 Sam Mestas                      |   1
 4623 - 27290 Jay Kim                         |   1
 5997 - 65283 AW Services Inc.                |   1
 2092 - 61288 Sbeih company                   |   1
 1469 - 64126 Omar Jada                       |   1
 2733 - 74600 Benny Jona                      |   1
 2192 - 73487 Zeymane Corp                    |   1
 5006 - 39261 Salifu Bawa                     |   1
 3556 - 36214 RC Andrews Cab                  |   1
 3721 - Santamaria Express, Alvaro Santamaria |   1
 2809 - 95474 C & D Cab Co Inc.               |   1
 2241 - 44667 - Felman Corp, Manuel Alonso    |   1
 3620 - 52292 David K. Cab Corp.              |   1
 2823 - 73307 Lee Express Inc                 |   1
 6057 - 24657 Richard Addo                    |   1
 6742 - 83735 Tasha ride inc                  |   1
 1085 - 72312 N and W Cab Co                  |   1
 3591 - 63480 Chuks Cab                       |   1
 0118 - 42111 Godfrey S.Awir                  |   1
 6574 - Babylon Express Inc.                  |   1
 3094 - 24059 G.L.B. Cab Co                   |   1
 5874 - 73628 Sergey Cab Corp.                |   1
 6743 - 78771 Luhak Corp                      |   1
 5074 - 54002 Ahzmi Inc                       |   1
 3623 - 72222 Arrington Enterprises           |   1
 4053 - 40193 Adwar H. Nikola                 |   1
 Chicago Star Taxicab                         |   1
 3011 - 66308 JBL Cab Inc.                    |   1
```

</details>

2. Запрос:

```bash
SELECT
  company_name,
  COUNT(cab_id) AS cnt
FROM
  cabs
GROUP BY
  company_name
HAVING
  COUNT(cab_id) < 100
ORDER BY
  cnt DESC;
```

[Наверх](#up)

### Задание 5

В приложении такси рассчитывается коэффициент стоимости поездки. Если погода хорошая, значение коэффициента равно 1. Если на улице дождь или шторм, коэффициент повышается до 2. У команды есть гипотеза, что в расчётах коэффициента ошибка. Чтобы проверить расчёт коэффициента, команде нужна выборка данных: разработчик может сверить коэффицент с данными в логах и исправить баг. Твоя задача — получить выборку.

Чтобы это сделать:
1. Получи описание погодных условий из таблицы `weather_records` для каждого часа.
2. Раздели все часы на две группы оператором CASE: 'Bad', если поле `description` содержит слова rain или storm; 'Good' для всех остальных.
3. Полученное поле назови `weather_conditions`.

В результирующей таблице должно быть два поля — дата и час (`ts`) и `weather_conditions`.

Сделай выборку за период с 2017-11-05 00:00 по 2017-11-06 00:00.

В ответе приложи:
1. Полученную таблицу с данными за указанный период.
2. Запрос, которым удалось решить задачу.

### Решение

<details>
<summary>1. Таблица с данными за указанный период.</summary>

```bash
         ts          | weather_conditions 
---------------------+--------------------
 2017-11-05 00:00:00 | Good
 2017-11-05 01:00:00 | Bad
 2017-11-05 02:00:00 | Good
 2017-11-05 03:00:00 | Good
 2017-11-05 04:00:00 | Bad
 2017-11-05 05:00:00 | Bad
 2017-11-05 06:00:00 | Good
 2017-11-05 07:00:00 | Good
 2017-11-05 08:00:00 | Good
 2017-11-05 09:00:00 | Good
 2017-11-05 10:00:00 | Good
 2017-11-05 11:00:00 | Good
 2017-11-05 12:00:00 | Good
 2017-11-05 13:00:00 | Good
 2017-11-05 14:00:00 | Bad
 2017-11-05 15:00:00 | Good
 2017-11-05 16:00:00 | Bad
 2017-11-05 17:00:00 | Good
 2017-11-05 18:00:00 | Bad
 2017-11-05 19:00:00 | Bad
 2017-11-05 20:00:00 | Bad
 2017-11-05 21:00:00 | Good
 2017-11-05 22:00:00 | Good
 2017-11-05 23:00:00 | Good
 2017-11-06 00:00:00 | Good
```

</details>

2. Запрос:

```bash
SELECT
  ts,
  CASE
    WHEN description LIKE '%rain%' OR description LIKE '%storm%' THEN 'Bad'
    ELSE 'Good'
  END AS weather_conditions
FROM
  weather_records
WHERE
  ts BETWEEN '2017-11-05 00:00:00' AND '2017-11-06 00:00:00';
```

[Наверх](#up)

### Задание 6

После обновления ПО таксопарки стали сообщать, что прибыль, которую они получают, не сходится с данными, которые отдаёт приложение. Разработка предполагает, что проблема может быть в данных о количестве поездок.

Чтобы определить, есть ли баг, нужно получить выборку с количеством поездок каждого таксопарка за 15 и 16 ноября 2017 года.

1. Выведи поле `company_name`. Поле с числом поездок назови `trips_amount` и выведи его.
2. Результаты, полученные в поле `trips_amount`, отсортируй по убыванию.

Подсказка: чтобы решить задачу, соедини таблицы `cabs` и `trips`. Примени агрегирующие функции с группировкой. Не забудь написать конструкцию с условием.

В ответе приложи:
1. Полученную таблицу с данными за указанный период.
2. Запрос, которым удалось решить задачу.

### Решение

<details>
<summary>1. Таблица с данными за указанный период.</summary>

```bash
                 company_name                 | trips_amount 
----------------------------------------------+--------------
 Flash Cab                                    |        19558
 Taxi Affiliation Services                    |        11422
 Medallion Leasin                             |        10367
 Yellow Cab                                   |         9888
 Taxi Affiliation Service Yellow              |         9299
 Chicago Carriage Cab Corp                    |         9181
 City Service                                 |         8448
 Sun Taxi                                     |         7701
 Star North Management LLC                    |         7455
 Blue Ribbon Taxi Association Inc.            |         5953
 Choice Taxi Association                      |         5015
 Globe Taxi                                   |         4383
 Dispatch Taxi Affiliation                    |         3355
 Nova Taxi Affiliation Llc                    |         3175
 Patriot Taxi Dba Peace Taxi Associat         |         2235
 Checker Taxi Affiliation                     |         2216
 Blue Diamond                                 |         2070
 Chicago Medallion Management                 |         1955
 24 Seven Taxi                                |         1775
 Chicago Medallion Leasing INC                |         1607
 Checker Taxi                                 |         1486
 American United                              |         1404
 Chicago Independents                         |         1296
 KOAM Taxi Association                        |         1259
 Chicago Taxicab                              |         1014
 Top Cab Affiliation                          |          978
 Gold Coast Taxi                              |          428
 Service Taxi Association                     |          402
 5 Star Taxi                                  |          310
 303 Taxi                                     |          250
 Setare Inc                                   |          230
 American United Taxi Affiliation             |          210
 Leonard Cab Co                               |          147
 Metro Jet Taxi A                             |          146
 Norshore Cab                                 |          127
 6742 - 83735 Tasha ride inc                  |           39
 3591 - 63480 Chuks Cab                       |           37
 1469 - 64126 Omar Jada                       |           36
 6743 - 78771 Luhak Corp                      |           33
 0118 - 42111 Godfrey S.Awir                  |           33
 6574 - Babylon Express Inc.                  |           31
 Chicago Star Taxicab                         |           29
 1085 - 72312 N and W Cab Co                  |           29
 2809 - 95474 C & D Cab Co Inc.               |           29
 2092 - 61288 Sbeih company                   |           27
 3011 - 66308 JBL Cab Inc.                    |           25
 3620 - 52292 David K. Cab Corp.              |           21
 4615 - 83503 Tyrone Henderson                |           21
 3623 - 72222 Arrington Enterprises           |           20
 5074 - 54002 Ahzmi Inc                       |           16
 2823 - 73307 Lee Express Inc                 |           15
 4623 - 27290 Jay Kim                         |           15
 3721 - Santamaria Express, Alvaro Santamaria |           14
 5006 - 39261 Salifu Bawa                     |           14
 2192 - 73487 Zeymane Corp                    |           14
 6057 - 24657 Richard Addo                    |           13
 5997 - 65283 AW Services Inc.                |           12
 Metro Group                                  |           11
 5062 - 34841 Sam Mestas                      |            8
 4053 - 40193 Adwar H. Nikola                 |            7
 2733 - 74600 Benny Jona                      |            7
 5874 - 73628 Sergey Cab Corp.                |            5
 2241 - 44667 - Felman Corp, Manuel Alonso    |            3
 3556 - 36214 RC Andrews Cab                  |            2
```

</details>

2. Запрос:

```bash
SELECT
  cabs.company_name AS company_name,
  COUNT(trips.trip_id) AS trips_amount
FROM
  cabs
INNER JOIN trips ON trips.cab_id = cabs.cab_id
WHERE
  CAST(trips.start_ts AS date) BETWEEN '2017-11-15' AND '2017-11-16'
GROUP BY
  company_name
ORDER BY
  trips_amount DESC;
```

[Наверх](#up)

## <a name="test-automation" />Основы автоматизации тестирования (JavaScript, NodeJS, Puppeteer)

### Задание 1

Автоматизируй тест-кейс для Яндекс.Маршрутов. Найди нужные селекторы на стенде: <https://qa-routes.praktikum-services.ru/>

```
[CASE-1] Проверка названия вида транспорта в результате для такси

Шаги:
1. Ввести «Время начала поездки» — 08:00.
2. В поле «Откуда»: Усачева, 3.
3. В поле «Куда»: Комсомольский проспект, 18.
4. Выбрать режим «Свой».
5. Выбрать вид транспорта: такси.

ОР: Текст появившегося результата начинается со слова «Такси».
```

### Решение

Селекторы:

| Элемент  | Селектор  |
|:----------|:----------|
| Поле «Часы»    | #form-input-hour    |
| Поле «Минуты»    | #form-input-minute    |
| Поле «Откуда»    | #form-input-from    |
| Поле «Куда»    | #form-input-to    |
| Режим «Свой»    | #form-mode-custom    |
| Транспорт «Такси»    | #from-type-taxi    |
| Строка результата    | #result-time-price    |

Автотест:

```javascript
const puppeteer = require('puppeteer');

const URL_TEST = 'https://qa-routes.praktikum-services.ru/';

async function testTaxiResult() {
    console.log('Запуск браузера');
    const browser = await puppeteer.launch({headless: false, slowMo: 100});

    console.log('Создание новой вкладки в браузере');
    const page = await browser.newPage();

    console.log('Переход по ссылке');
    await page.goto(URL_TEST);

    console.log('Шаг 1: ввод часов и минут');
    const hoursInput = await page.$('#form-input-hour');
    await hoursInput.type('08');

    const minutesInput = await page.$('#form-input-minute');
    await minutesInput.type('00');

    console.log('Шаг 2: заполнение поля Откуда');
    const fromInput = await page.$('#form-input-from');
    await fromInput.type('Усачева, 3');

    console.log('Шаг 3: заполнение поля Куда');
    const toInput = await page.$('#form-input-to');
    await toInput.type('Комсомольский проспект, 18');

    console.log('Шаг 4: выбор режима Свой');
    const routeMode = await page.$('#form-mode-custom');
    await routeMode.click();

    console.log('Шаг 5: выбор вида транспорта');
    const typeOfTransport = await page.$('#from-type-taxi');
    await typeOfTransport.click();

    console.log('Ожидание элемента с результатом');
    await page.waitForSelector('#result-time-price')

    console.log('Получение строки с результатом');
    const text = await page.$eval('#result-time-price', element => element.textContent);

    console.log('Проверка условия тест-кейса');
        if (text.startsWith('Такси')) {
        console.log('Успех. Текст содержит: ' + text);
    } else {
          console.log(`Ошибка. Текст не начинается со слова 'Такси'`)
    }

    console.log('Закрытие браузера');
    await browser.close();
}

testTaxiResult();
```

[Наверх](#up)

### Задание 2

Автоматизируй тест-кейс для [ya.ru](ya.ru), применив нужные селекторы.

```
[CASE-2] Проверка появления результатов поиска

Предусловие:
Перейти на страницу ya.ru.

Шаги:
1. Ввести «Автоматизация тестирования» в поисковую строку.
2. Нажать кнопку «Найти».

ОР: Выполнен переход на страницу выдачи поиска и результат поиска непустой.
```

### Решение

Селекторы:

| Элемент  | Селектор  | 
|:----------|:----------|
| Поисковая строка    | #text    |
| Кнопка «Найти»    | .button[type=submit]    |
| Результат поиска	    | .serp-item    |

Автотест:

```javascript
const puppeteer = require('puppeteer');

async function testYaRu() {
    console.log('Запуск браузера');
    const browser = await puppeteer.launch();

    console.log('Создание новой вкладки в браузере');
    const page = await browser.newPage();

    console.log('Переход на страницу ya.ru');
    await page.goto('https://ya.ru/');

    console.log('Ввод текста "Автоматизация тестирования" в поисковую строку');
    const searchField = await page.$('#text');
    await searchField.type('Автоматизация тестирования');

    console.log('Клик в кнопку "Найти"');
    const searchButton = await page.$('.button[type=submit]');
    await searchButton.click();
    
    console.log('Ожидание перехода в страницу поисковых результатов');
    await page.waitForNavigation();
    
    console.log('Получение элементов результата поиска');
    const result = await page.$('.serp-item');
    
    console.log('Сравнение ОР и ФР');
    if (result == null) {
        console.log('Результаты поиска не найдены');
    } else {
        console.log('Результаты поиска отобразились');
    }
    
    console.log('Закрытие браузера');
    await browser.close();
}

testYaRu();
```

[Наверх](#up)

