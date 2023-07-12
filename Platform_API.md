## Adserving API

	API доступно по адресу https://platform.adserving.ru/api

Для работы через API необходимо получить Token методом /api/login. Для авторизации через полученный токен используется заголовок Bearer Token.

```
Authorization: Bearer poKwGAWsyE!FQy33OPsOM4CU_5kQ#TzIN6RGcSpBhfCiZ*ZhzOVzw9GgGhaQXl!h
```

### Получение токена

	POST /login

Для получения Token необходимо использовать логин и пароль от личного кабинета https://platform.adserving.ru. Token выдается на 45 дней и должен быть перегенерирован этим методом каждые 45 дней.

Запрос Token:

```
{
	"login":"логин_от_личного_кабинета",
	"password":"пароль_от_личного_кабинета"
}
```

Ответ:
```
{
	"token":"poKwGAWsyE!FQy33OPsOM4CU_5kQ#TzIN6RGcSpBhfCiZ*ZhzOVzw9GgGhaQXl!h"
}
```

Ошибка авторизации:
```
{
	"report_id":"-1",
	"message":"Unloginned user"
}
```

### Отчеты

#### Запрос генерации отчета

	POST /api/reports/generate

Пример: https://platform.adserving.ru/api/reports/generate

Для запроса необходимо передать JSON объект, полученный из кабинета https://platform.adserving.ru/. Для этого вы настраиваете все поля отчета в кабинете. После этого нажимаете кнопку "GET API JSON". В буфер обмена будет скопирован JSON объект, который необходимо использовать для запроса отчета:

```
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
В запросе указываются следующие объекты:

```
Период отчета:

"timeRange": {
	"timeZone": "Europe/Moscow",
	"type": "Custom",
	"dataStartTimestamp": "2023-05-27T00:00:00.000Z",
	"dataEndTimestamp": "2023-06-25T23:59:00.000Z"
}

timeZone - тайм зона для генерации отчета;
type - тип отчета, вcегда используетcя Custom;
dataStartTimestamp - дата начала периода отчета;
dataEndTimestamp - дата конца периода отчета.
```

```
Способ получения отчета:

"reportDeliveryMethods": [{
	"type": "none",
	"exportFileType": "excel",
	"compressionType": "none",
	"emailRecipients": ["example@domain.com"],
	"exportFileNamePrefix": "test123",
	"appendTimestampToReportName": false
}]

type - всегдя none
exportFileType - тип отчета excel/csv;
compressionType - архивация отчета none/zip;
emailRecipients - способ получения example@domain.com - отправить на email / none - отчет будет доступен для скачивания через  API  или из https://platform.adserving.ru/#/spa/analytics/report-builder/report-history/main
exportFileNamePrefix - текст, который будет добавлен к названию отчета;
appendTimestampToReportName - добавлениe timestamp в название отчета true/false.
```

```
Набор атрибутов и метрик в отчете:

"reportStructure": {
	"attributeIDs": ["Account Name"],
	"metricIDs": ["impressions Gross"],
	"attributeIDsOnColumns": [],
	"timeBreakdown": "day"
}

attributeIDs - массив атрибутов;
metricIDs - массив метрик;
attributeIDsOnColumns - пустой массив;
timeBreakdown - группировка по дате day/week/month/year/total.
```

```
Фильтры по плейсментам и сайтам:

"filters": {
	"placements": [],
	"sites": []
}

placements - массив плейсментов в отчете. Пустой массив = все плейсменты;
sites - массив сайтов в отчете. Пустой массив = все сайты.
```

Ответ:

```
{
    "report_id": "a70bf4f6229f792191bdd9f5cdfe99e1",
    "message": "The report is added to queue!"
}
````

Ошибки:

```
{
    "report_id": "-1",
    "message": "Error: the report has a wrong format!"
}
```

Ошибка авторизации:
```
{
	"report_id":"-1",
	"message":"Unloginned user"
}
```

### Получение списка сренерированных отчетов

	GET /api/reports/list 

Пример: https://platform.adserving.ru/api/report/list 

Ответ:

```
[
    ["0", "report_1.xslx", "Aggregated Report", "2023-06-27 11:56:07", "-", "test123", "once", "a70bf4f6229f792191bdd9f5cdfe99e1"],
    ["2", "report_2.xslx", "Aggregated Report", "2023-06-13 11:56:16", "-", "test123", "once", "fa80fcf3e71fd159a0d1b8b2ca5e20fa"]
]

0 - статус генерации отчета [0 - отчет в очереди, 1 - отчет готов, 2 - генерация отчета];
report_1.xslx - ссылка на файл сегенерированного отчета, доступна через web при условии, что вы залогинены в кабинет;
Aggregated Report - тип отчета;
2023-06-27 11:56:07 - дата и время запроса генерации отчета;
- - 
test123 - название отчета;
a70bf4f6229f792191bdd9f5cdfe99e1 - ID отчета
```


Ошибка авторизации:

```
{
	"report_id":"-1",
	"message":"Unloginned user"
}
```

### Получение отчета

	GET	/api/reports/get/идентификатор_отчета

**Идентификатор_отчета** - полученный идентфикатор отчета методом api/reports/get или /api/reports/list. Идентификатор_отчета имеет вид "fa80fcf3e71fd159a0d1b8b2ca5e20fa".

Ошибка авторизации:

```
{
	"report_id":"-1",
	"message":"Unloginned user"
}