# RDF: Файл данных интеракций - Interaction File

[< Файлы сырых данных (RDF - Raw Data File)](../RDF.md)

Описание полей:
В следующей таблице описаны поля канала взаимодействия (RDF).

|Название|Описание|Тип|
|-|-|-|
|CampaignID|Уникальный идентификатор кампании Adserving.|Integer|
|EntityID|Уникальный идентификатор объявления, с которым взаимодействовал пользователь, назначенный Adserving.|Integer|
|EventTypeID|Уникальный идентификатор типа события, который будет отображаться в ленте взаимодействия в файле метаданных. Доступны следующие варианты, соответствующие агрегированные метрики отчетов указаны в скобках:</br> 4: System Interaction (нет данных) </br> 5:  Video Interaction (сумма основных показателей видео, не включая показатели)</br>  6: Custom Interaction (общее количество пользовательских взаимодействий) </br> 7: Panel (показы с любым расширением панели, инициированным пользователем + показы с определенным расширением панели, инициированным пользователем)|Integer|
|InteractionDate|Дата, когда пользователь взаимодействовал с объявлением. Формат: Year-Month-Day / Hour:Minute:Second|DATETIME|
|InteractionID|Уникальный идентификатор объекта взаимодействия Adserving.|String(200) |
|PlacementID|Уникальный идентификатор места размещения объявления.|Integer|
|SiteID|ID сайта паблишера.|Integer|
|AccountID|Уникальный идентификатор аккаунта Adserving.|Integer|
|AdvertiserID|Уникальный идентификатор рекламодателя Adserving.|Integer|
|BrandID|Уникальный идентификатор бренда Adserving.|Integer|
|DeliveryGroupId|Уникальный идентификатор группы рекламных объявлений Adserving.|Integer|
|InteractionDuration|Длительность взаимодействия в секундах.|Integer|
|IP|IP пользовательского устройства, вызвавшего событие. Примечание. В соответствии с регламентом GDPR последний октет IP-адреса усекается. Это поле пусто для немецких IP-адресов.|String (16)|
|PanelID|ID панели Adserving.|Integer|
|PCP|Пользовательский параметр паблишера (PCP). Параметр, определенный для паблишера/сайта. Появляется только в том случае, если PCP существует.|String(2048)|
|Referrer|URL-адрес, полученный из поля реферера HTTP-заголовка в процессе показа/отслеживания рекламы. Может быть URL-адресом страницы, на которой появилось объявление, URL-адресом рекламного сервера или пустым, если оно не было передано.|String|
|SessionID|Уникальный идентификатор сеанса. Позволяет связать показ, клик и взаимодействие, принадлежащие одному сеансу.|Integer|
|TargetAudienceID|Уникальный идентификатор аудитории, указанный в стандартном фиде.|Integer|
|UserID|Уникальный идентификатор пользователя Adserving (Stable ID).|String(36)|
|VersionID|Применяется к динамическим креативным объявлениям. Уникальный идентификационный номер генерируется для каждой новой версии Adserving.|Integer|
|VideoAssetID|Уникальный идентификатор видеоресурса, назначенный Adserving.|Integer|
|UserConsent|Закодированная строка с сайта паблишера, определяющая поставщиков и цели, на которые пользователь дает согласие.|String|