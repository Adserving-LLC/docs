# Adserving Platform API

[< К оглавлению](README.md)

Эндпоинт сервиса API:

```text
https://platform.adserving.ru/api
```

Обратите внимание, если у вас доступ к [ЛК](https://lk.adserving.ru/), то следует указывать следующий эндпоинт:

```text
https://lk.adserving.ru/api
```

## Получение токена

```
POST /login
```

Для работы через API необходимо получить `token`. Этот токен должен использоваться в заголовке `Bearer Token` для всех
последующих запросов к API.

Чтобы получить `token` необходимо использовать логин и пароль от [Платформы](https://platform.adserving.ru) (
или [ЛК](https://lk.adserving.ru), если у вас есть к нему доступ). Токен действителен в течение 45 дней с момента
создания.

Пример тела запроса токена:

```json
{
   "login":"логин_от_личного_кабинета",
   "password":"пароль_от_личного_кабинета"
}
```

Пример ответа сервиса:

```json
{
   "token":"poKwGAWsyE!FQy33OPsOM4CU_5kQ#TzIN6RGcSpBhfCiZ*ZhzOVzw9GgGhaQXl!h"
}
```

Пример ошибки авторизации:

```json
{
   "report_id":"-1",
   "message":"Unloginned user"
}
```

## Создание отчета

```text
POST /report/generate
```

В качестве тела запроса необходимо передать JSON объект, полученный из вашего кабинета. Для этого вы настраиваете все
поля отчета в кабинете. После этого нажимаете кнопку `GET API JSON`.

!["GET API JSON"](imgs/get_api_json_button.jpg).

Пример JSON объекта для создания отчета:

```json
{
    "entities": [{
        "type": "AnalyticsReport",
        "reportName": "test123",
        "reportScope": {
            "entitiesHierarchy": {
                "entitiesHierarchyLevelType": "ACCOUNT",
                "accountContext": 0,
                "accounts": [1000056372],
                "advertisers": [],
                "displayCampaignsIds": [],
                "searchCampaignsIds": [],
                "sites": [],
                "campaignsType": ["Display"]
            },
            "filters": {
                "placements": [],
                "sites": []
            },
            "timeRange": {
                "timeZone": "Europe/Moscow",
                "type": "Custom",
                "dataStartTimestamp": "2023-05-27T00:00:00.000Z",
                "dataEndTimestamp": "2023-06-25T23:59:00.000Z"
            },
            "presetId": null
        },
        "reportStructure": {
            "attributeIDs": ["Account Name"],
            "metricIDs": ["impressions Gross"],
            "attributeIDsOnColumns": [],
            "timeBreakdown": "day"
        },
        "reportExecution": {
            "type": "Ad_Hoc"
        },
        "reportDeliveryMethods": [{
            "type": "none",
            "exportFileType": "excel",
            "compressionType": "none",
            "emailRecipients": ["example@domain.com"],
            "exportFileNamePrefix": "test123",
            "appendTimestampToReportName": false
        }],
        "reportAuthorization": {
            "type": "mm3",
            "userID": 0,
            "ownerAccountId": 0
        }
    }]
}
```

### timeRange (период отчета)

| Свойство             | Тип      | Значение по умолчанию | Описание                                 |
|----------------------|----------|-----------------------|------------------------------------------|
| `timeZone`           | `String` | `Europe/Moscow`       | Часовой пояс отчета                      |
| `type`               | `String` | `Custom`              | Тип отчета, вcегда используетcя `Custom` |
| `dataStartTimestamp` | `String` |                       | Дата начала периода отчета               |
| `dataEndTimestamp`   | `String` |                       | Дата конца периода отчета                |

### reportDeliveryMethods (способ получения отчета)

| Свойство                      | Тип                 | Значение по умолчанию | Описание                                                                                                                                                                                                                                                                                                                                                          |
|-------------------------------|---------------------|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`                        | `String`            | `none`                | Всегда одно значение                                                                                                                                                                                                                                                                                                                                              |
| `exportFileType`              | `String`            | `excel`               | Тип отчета excel/csv                                                                                                                                                                                                                                                                                                                                              |
| `compressionType`             | `String`            | `none`                | Сжатие отчета:<br/>`none` - без сжатия (подходит для небольших отчетов);<br/>`zip` - сжатие в zip архив                                                                                                                                                                                                                                                           |
| `emailRecipients`             | `[]String`,`String` |                       | Массив почтовых адресов, на которые будет отправлен готовый отчет. <br/>Если указать `none`, отчет будет доступен для скачивания через API или из вашего личного кабинета (в [Platform](https://platform.adserving.ru/#/spa/analytics/report-builder/report-history/main) или в [ЛК](https://lk.adserving.ru/#/spa/analytics/report-builder/report-history/main)) |
| `exportFileNamePrefix`        | `String`            |                       | Текст, который будет добавлен в начало имени файла отчета                                                                                                                                                                                                                                                                                                         |
| `appendTimestampToReportName` | `Boolean`           | `false`               | Добавляет timestamp в название отчета                                                                                                                                                                                                                                                                                                                             |

### reportStructure (набор атрибутов и метрик в отчете)

| Свойство                | Тип        | Значение по умолчанию | Описание                                                         |
|-------------------------|------------|-----------------------|------------------------------------------------------------------|
| `attributeIDs`          | `[]String` |                       | Массив атрибутов                                                 |
| `metricIDs`             | `[]String` |                       | Массив метрик                                                    |
| `attributeIDsOnColumns` | `[]Int32`  | `[]`                  | Оставьте пустой массив                                           |
| `timeBreakdown`         | `String`   | `day`                 | Группировка данных по дате (`day`,`week`,`month`,`year`,`total`) |

### filters (фильтры по плейсментам и сайтам)

| Свойство     | Тип       | Значение по умолчанию | Описание                                                                                             |
|--------------|-----------|-----------------------|------------------------------------------------------------------------------------------------------|
| `placements` | `[]Int32` | `[]`                  | Массив плейсментов по которым выбираются данные. Оставьте массив пустым, что выбрать все плейсменты. |
| `sites`      | `[]Int32` | `[]`                  | Массив сайтов  по которым выбираются данные. Оставьте массив пустым, что выбрать все сайты.          |

Пример успешного ответа:

```json
{
   "report_id": "a70bf4f6229f792191bdd9f5cdfe99e1",
   "message": "The report is added to queue!"
}
````

Пример ошибки:

```json
{
   "report_id": "-1",
   "message": "Error: the report has a wrong format!"
}
```

Пример ошибки авторизации:

```json
{
   "report_id":"-1",
   "message":"Unloginned user"
}
```

## Получение списка сгенерированных отчетов

```text
GET /reports/list
```

Пример успешного ответа:

```json
[
   ["0", "report_1.xslx", "Aggregated Report", "2023-06-27 11:56:07", "-", "test123", "once", "a70bf4f6229f792191bdd9f5cdfe99e1"],
   ["2", "report_2.xslx", "Aggregated Report", "2023-06-13 11:56:16", "-", "test123", "once", "fa80fcf3e71fd159a0d1b8b2ca5e20fa"]
]
````

| Порядковы номер в массиве | Тип      | Описание                                                                                            |
|:-------------------------:|----------|-----------------------------------------------------------------------------------------------------|
|             0             | `String` | Статус генерации отчета<br/>`0` - отчет в очереди;<br/>`1` - отчет готов;<br/>`2` - генерация отчета|
|             1             | `String` | Ссылка на файл отчета                                                                               |
|             2             | `String` | Тип отчета                                                                                          |
|             3             | `String` | Дата и время запроса на генерацию отчета                                                            |
|             4             | `String` |                                                                                                     |
|             5             | `String` |                                                                                                     |
|             6             | `String` | Периодичность выгрузки отчета (всегда `once`)                                                       |
|             7             | `String` | ID отчета                                                                              |

Пример ошибки:

```json
{
   "report_id": "-1",
   "message": "Error: the report has a wrong format!"
}
```

Пример ошибки авторизации:

```json
{
   "report_id":"-1",
   "message":"Unloginned user"
}
```

### Скачивание отчета

```text
GET /report/get/<ID>
```

Вместо `<ID>` нужно указать идентификатор отчета (_см. [Получение списка сгенерированных отчетов](#Получение_списка_сренерированных_отчетов)_).
В случае успешного запроса, начнется скачивание файла.

