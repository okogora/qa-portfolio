# <a name="up" />Выполненные проекты

[Проектирование тестов](#test-design)

[Тестирование веб-приложений](#web-testing)

[Тестирование мобильных приложений](#mobile-testing)

[Тестирование API](#api-testing)

[Основы баз данных](#data-bases)

[Основы автоматизации тестирования](#test-automation)

## <a name="test-design" />Проектирование тестов

#### Задание

[Наверх](#up)

## <a name="web-testing" />Тестирование веб-приложений

#### Задание

[Наверх](#up)

## <a name="mobile-testing" />Тестирование мобильных приложений

#### Задание

[Наверх](#up)

## <a name="api-testing" />Тестирование API

#### Задание

[Наверх](#up)

## <a name="data-bases" />Основы баз данных (PostgreSQL)

#### Задание 1

От разработчиков поступила задача: нужно выяснить, какие запросы шли на IP-адреса. IP-адрес состоит из четырёх чисел, они разделены точками. Тебе нужны адреса, которые начинаются с "233.201.".

Логи лежат на удалённом сервере по адресу logs/2019/12. День, когда случилась ошибка, неизвестен.

Твоя задача — узнать, какие запросы были отправлены.

В ответе приложи:
1. Команду, которой тебе удалось получить нужные логи.
2. Подходящие строки, например:

```bash
184.79.247.161 - - [30/12/2019:21:38:13 +0000] "PUT /alerts HTTP/1.1" 400 3557
```

***

#### Решение

1. Команда:

```bash
grep ^233.201 /logs/2019/12/*.txt
```

2. Логи:

```bash
233.201.188.154 - - [18/12/2019:21:46:01 +0000] "DELETE /events HTTP/1.1" 403 3971
233.201.182.9 - - [21/12/2019:21:56:20 +0000] "PATCH /users HTTP/1.1" 400 4118
```

***

#### Задание 2

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

***

#### Решение

1. Команды, которые создают директории bug1 и events.

```bash
mkdir bug1
mkdir events
```

2. Команда, которой выбираешь запросы за указанный период. Это те запросы, которыми ты отбираешь логи в файл main.txt.

```bash
grep "21:3" ~/logs/2019/12/apache_2019-12-30.txt > ~/bug1/main.txt
grep "21:3" ~/logs/2019/12/apache_2019-12-31.txt >> ~/bug1/main.txt
```

3. Команды, которыми ты кладёшь логи в файлы 400.txt и 500.txt из main.txt.

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

***

#### Задание 3

У тебя есть база данных с поездками на такси. По плану на линию обслуживания должно было выйти 10550 автомобилей — эта цифра покрывает спрос пользователей. Команде поступило много жалоб — свободных автомобилей оказалось недостаточно. Сколько такси вышло на линии на самом деле? Информация о всех машинах на линии есть в таблице `cabs`.
1. Зайди на удалённый сервер.
2. Подключись к базе данных `chicago_taxi`.
3. Посчитай, сколько всего автомобилей в таблице `cabs`.

В ответе приложи:
1. Число автомобилей
2. Запрос, которым тебе удалось решить задачу.

***

#### Решение

1. Число автомобилей: 5529.
2. Запрос:

```bash
SELECT
  COUNT(*) AS cnt
FROM cabs;
```
[Наверх](#up)

## <a name="test-automation" />Основы автоматизации тестирования (JavaScript, NodeJS, Puppeteer)

#### Задание 1

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
***

#### Решение

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

```js
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

***

#### Задание 2

Автоматизируй тест-кейс для [ya.ru](https://ya.ru), применив нужные селекторы.


```
[CASE-2] Проверка появления результатов поиска

Предусловие:
Перейти на страницу ya.ru.

Шаги:
1. Ввести «Автоматизация тестирования» в поисковую строку.
2. Нажать кнопку «Найти».

ОР: Выполнен переход на страницу выдачи поиска и результат поиска непустой.
```

***

#### Решение

Селекторы:

| Элемент  | Селектор  | 
|:----------|:----------|
| Поисковая строка    | #text    |
| Кнопка «Найти»    | .button[type=submit]    |
| Результат поиска	    | .serp-item    |

Автотест:

```js
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
