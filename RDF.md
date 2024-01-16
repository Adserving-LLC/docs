# Файлы сырых данных (RDF - Raw Data File)

[< К оглавлению](README.md)

Adserving предоставляет 4 типа файлов:
1. [Стандартный](RDF/StandardFile.md) - содержит метрики Impression Net и Click Net с подробными дынными по каждому событию;
2. [Файл данных интеракций](RDF/InteractionFile.md) - содержит все прочие метрики, кроме Impression Net и Click Net, такие, как видимость, квартили и прочие;
3. [Конверсионный](RDF/ConversionFile.md) - содержит конверсии с подробными параметрами ;
4. [Файлы сущностей](RDF/MatchFiles.md) - 23 файла, содержащие подробное описание каждой сущности, идентификаторы которых встречаются в предыдущих 3 типах файлов.

Файлы сырых данных, далее `RDF`, предоставляются каждый час и содержат в себе данные конкретного часа в формате CSV. Задержка данных около 4-х часов с момента наступления события. Файлы сущностей, далее `Match` файлы, предоставляются в виде одного ZIP архива, остальные 3 файлы каждый в своем ZIP архиве.

Файлы выкладываются на FTP сервис [ftp.adserving.ru](ftp://ftp.adserving.ru) либо могут загружаться на FTP/sFTP/S3 ресурсы клиента.

## Правила формирования имени файла

RDF файлы имеют следующий формат имени: Adserving_RDF_<Data Feed>_<Entity Level>_<EntityID>_<Date_From>_<Date_To>.csv

|Элемент|Описание|
|-|-|
|Data Feed|Возможные значения: Standard, Interaction, Conversion, SiteActivity |
|Entity Level|В зависимости от данных, по которым генерируются RDF файлы, значения могут быть: Account, Advertiser, Campaign. Если выбрано несколько сущностей, например, несколько Advertisers, то Data Feed будет преобразован в сущность выше по иерархии, например для Advertisers это будет Account.|
|Entity ID|В зависимости от сущности Data Feed, это может быть: Account ID, Advertiser ID или Campaign ID|
|Date From/Date To|Значение даты и времени зависит от конктретного периода генерации отчетов. Файлы генерируются каждый час. Например, значения начала и конца периода для файлов в вашей папке за 05 Августа 2023, выгруженные между 14:00 и 15:00: Adserving_RDF_Conversion_Account_000_23080514_23080515|

Например, RDF, включающий всю возможную иформацию, генерирует следующие файлы каждый раз.

##### Adserving_RDF_Standard_Advertiser_1001_23080508_23080512.zip
    Adserving_RDF_Standard_Advertiser_1001_23080508_23080512_1.csv
    Adserving_RDF_Standard_Advertiser_1001_23080508_23080512_2.csv

##### Adserving_RDF_Interaction_Advertiser_1001_23080508_23080512.zip
    Adserving_RDF_Interaction_Advertiser_1001_23080508_23080512_1.csv
    Adserving_RDF_Interaction_Advertiser_1001_23080508_23080512_2.csv
    Adserving_RDF_Interaction_Advertiser_1001_23080508_23080512_3.csv

##### Adserving_RDF_Conversion_Advertiser_1001_23080508_23080512.zip
    Adserving_RDF_Conversion_Advertiser_1001_23080508_23080512.csv

##### Adserving_RDF_SiteActivity_Advertiser_1001_23080508_23080512.zip
    Adserving_RDF_SiteActivity_Advertiser_1001_23080508_23080512.csv

##### Adserving_RDF_Match_Advertiser_1001_23080508_23080512.zip
    Adserving_RDF_Match_AccountsMatchFile_Advertiser_1001_23080508_23080512.csv
    Adserving_RDF_Match_AdvertisersMatchFile_Advertiser_1001_23080508_23080512.csv

## Файлы сущностей - Match Files

Формат имени файла - `Adserving_RDF_Match_[Entity_Type]_[Entity_ID]_[Date][Hour_From]_[Date][Hour_To].zip`, где
```
[Entity_Type] - тип объединения данных, например Advertiser - данные по конкретному рекламодателю
[Entity_ID] - идентификатор сущности в базы Adserving, напрмиер 1001
[Date] - дата, данные за которую содержит файл, например 230530
[Hour_From] - час начала периода, например 04
[Hour_To] - час конца периода, например 05
```

[Подробное описание фалов сущностей и их полей для Match Files](RDF/MatchFiles.md)
