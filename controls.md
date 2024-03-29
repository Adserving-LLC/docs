# Настройка контролов показа VPAID для RuTube

[< К оглавлению](README.md)

Для показа можно настроить следующие контролы и их параметры:

* кнопка включения/выключения звука (mute)
* кнопка закрытия рекламного ролика
* время, через которое появится кнопка закрытия рекламного ролика
* позицию кнопки включения/выключения звука
* позицию кнопки закрытия рекламного ролика
* время задержки клика
* отображение кликовой области в виде кнопки
* постановка видео на паузу при клике
* закрытие креатива при клике
* позицию кнопки закрытия креатива
* включение плашки "Реклама" для соблюдения закона 347-ФЗ
* включение плашки "ЕРИД" для соблюдения закона 347-ФЗ

Если файл конфигурации не существует, контролы показаны не будут.

## Файл для настройки контролов

Для настройки контролов используется файл config.json. Файл config.json должен распологаться в той же директории, в которой находится видео файл. Это позволяет сделать настройку для конктерного видео.

### Структура файла config.json

```js
{
    "mute":"on",
    "mute_position":"bottom:100px;left:100px;",
    "close":"5",
    "close_position":"top:100px;right:100px;",
    "click_delay":"3",
    "close_on_click":"0",
    "pause_on_click":"0",
    "click_button":"1",
    "click_position":"right:5%;bottom:10%;",
    "adChoice":"Реклама",
    "adChoice_position":"right:5%;bottom:10%;",
    "erid":"on",
    "erid_position":"right:5%;bottom:10%;",
}
```

,где параметры отвечают за:

* **mute** (string) - отображение кнопки включения/выключения звука
* **mute_position** (string) - позицию кнопки включения/выключения звука
* **close** (integer) - отображение кнопки закрытия рекламного ролика
* **close_position** (string) - позицию кнопки закрытия рекламного ролика
* **click_delay** (integer) - задерка клика в секундах
* **close_on_click** (integer) - закрытие креатива при клике
* **pause_on_click** (integer) - пауза креатива при клике
* **click_button** (integer) - отображение кликовой области в виде кнопки
* **click_position** (string) - позицию кнопки клика
* **adChoice** (string) - отображение плашки с надписью, переданной в качетсве значения
* **adChoice_position** (string) - позицию плашки с надписью
* **erid** (string) - отображение плашки c с надписью `edid: abcd123456789`, значение передается через параметр lineid
* **erid_position** (string) - позицию плашки "ЕРИД"

## Настройка контролов

Все параметры в конфигурационном файле могут быть **пропущены**. Пропущенные параметры считаются установленным в значение **пусто** и будут восприняты как значение по умолчанию.

### Настройка кликовой области

По умолчанию, кликовая область прозрачная и занимает всю площадь креатива. Задержка клика составляет 3 секнду от старта видео. При клике по креативу он продолжит проигрываться.

Следующие настройки позволяют поменять поведение креатива при клике и отображение кликовой области:

|параметр|описание|значения|пример|
|---|---|---|---|
|click_delay|Настройка задержки клика|**пусто** - зажержка клике задержка равна 3 секундам.<br>**0** - нет задержки при клике<br>**больше 0** - клик по креативу будет возможен только через определенное в параметре число секунд.|"click_delay":"2"|
|click_button|Настройка отображения кликовой области|**пусто** - тоже самое, что 0.<br>**0** (не 1) - кликовая область прозрачная и занимает всю площадь креатива.<br>**1** - отображение в виде черной полупрозрачной кнопки с надписью "Перейти ->" со скругленными углами.|"click_button":"1"|
|click_position|Настройка позиции кнопки кликовой области. Применяется только если **click_button = 1**|**пусто** - кнопка отобразится в нижнем правом углу<br>**CSS позиционирование** - только для left / right / top / bottom, значения в пикселях или процентах.|"click_position":"right:5%;bottom:10%;"|
|pause_on_click|Поставить креатив на паузу при клике|**пусто** - тоже самое, что 0.<br>**0** - поставновки креатива на паузу при клике не произойдет<br>**1** - при клике креатив будет поставлен на паузу|"pause_on_click":"0",|
|close_on_click|Закрыть креатив при клике|**пусто** - тоже самое, что 0.<br>**0** - закрытия креатива при клике не произойдет<br>**1** - при клике креатив будет закрыт|"close_on_click":"0"|

### Настройка кнопки включения/выключения звука

Кнопка включения/выключения звука, по умолчанию, отображается в в нижнем левом углу.

Следующие настройки позволяют поменять отображение кнопки включения/выключения звука:

|параметр|описание|значения|пример|
|---|---|---|---|
|mute|Включение/выключение отображения кнопки управления звоком|**пусто** - тоже самое, что **off**<br>**on** - отображать кнопку включения/выключения звука<br>**off** - скрыть кнопку включения/выключения звука|"mute":"on"|
|mute_position|Настройка позиции кнопки включения/выключения звука|**пусто** - кнопка отобразится в нижнем левом углу<br>**CSS позиционирование** - только для left / right / top / bottom, значения в пикселях или процентах.|"mute_position":"bottom:100px;left:100px;"|

### Настройка кнопки закрытия рекламного ролика

Кнопка закрытия рекламного ролика по умолчению не отображена. При включении кнопки закрытия, она расположена в верхнем правом углу.

Следующие настройки позволяют поменять отображение кнопки закрытия рекламного ролика:

|параметр|описание|значения|пример|
|---|---|---|---|
|close|Включение/выключение отображения кнопки закрытия рекламного ролика|**пусто** - тоже самое, что **-1**<br>**-1** - кнопка закрытия рекламного ролика не отображается <br>**больше 0** - отображать кнопку закрытия рекламного ролика через определенное в параметре число секунд.|"close":"5"|
|close_position|Настройка позиции кнопки закрытия рекламного ролика|**пусто** - кнопка отобразится в верхнем правом углу<br>**CSS позиционирование** - только для left / right / top / bottom, значения в пикселях или процентах.|"close_position":"top:100px;right:100px;"|

### Настройка плашки "Реклама" для соблюдения закона 347-ФЗ

Плашка по умолчению не отображена. При включении плашкия, она расположена в верхнем левом углу.

Следующие настройки позволяют включить, поменять расположение, размер и текст для плашки "Реклама":

|параметр|описание|значения|пример|
|---|---|---|---|
|adChoice|Включение/выключение отображения плашки|**пусто** - тоже самое, что параметр пропущен - плашка не отображается <br>**Любой текст** - отображать плашкe "Реклама".|"adChoice":"Реклама"|
|adChoice_position|Настройка позиции и размера плашки|**пусто** - плашка отобразится в верхнем левом углу<br>**CSS позиционирование/размер** - только для left / right / top / bottom / width / height, значения в пикселях или процентах.|"adChoice_position":"top:100px;right:100px;width:200px;"|

### Настройка плашки "ЕРИД" для соблюдения закона 347-ФЗ

Плашка отображается в случае, если в код Adserving передано значение ЕРИД при вызове тега. Для передачи значения необходимо в GET-переменную `lineid` передать значение по следующим правилам:

* переданное любое значение не в виде GET-переменных считается значение ЕРИД
* передана как значение для GET-перпемнной `erid`

Примеры:

```
# Передана как единственное значение
https://bs.serving-sys.ru/Serving/adServer.bs?c=23&cn=display&pli=1041746801&ord=[timestamp]&pcp=$${site.id}:{request.referrer:urlenc}$$&lineid=$$sgn3532nsld$$

# Передана как значение GET-переменной erid
https://bs.serving-sys.ru/Serving/adServer.bs?c=23&cn=display&pli=1041746801&ord=[timestamp]&pcp=$${site.id}:{request.referrer:urlenc}$$&lineid=$$erid=sgn3532nsld$$

# Передана как значение GET-переменной erid вместе с другими значениями
https://bs.serving-sys.ru/Serving/adServer.bs?c=23&cn=display&pli=1041746801&ord=[timestamp]&pcp=$${site.id}:{request.referrer:urlenc}$$&lineid=$$ccc=ddd&erid=sgn3532nsld&aaa=bbb$$

```

Значение GET-переметра `lineid` рекомендовано оборачивать в символы `$$`, для того, чтоб при разборе переданных значений, наши коды правильно определяли польность переданный набор данных либо как GET-переменные, либо как значение с любым набором симоволо. Символы `$$` могут быть пропущены, если GET-переметр `lineid` передается urlencode значение.

По умолчению плашка "ЕРИД" оботражается, если передано значение и не отображена, если значение для ЕРИД не передано. По умолчанию плашкия "ЕРИД" она расположена в верхнем правом углу в виде круглой кнопки с "i" в центе. При клике по кнопке "i" раскрывается плашка с написью `edid: abcd123456789`.

Следующие настройки позволяют выключить, поменять расположение, размер и текст для плашки "Реклама":

|параметр|описание|значения|пример|
|---|---|---|---|
|erid|Выключение отображения плашки|**Пусто** - тоже самое, что параметр "on" - плашка отображается при передаче параметра "ЕРИД" <br>off - скрыть плашку "ЕРИД" в любом случае.|"erid":"off"|
|erid_position|Настройка позиции и размера плашки|**пусто** - плашка отобразится в верхнем правом углу<br>**CSS позиционирование/размер** - только для left / right / top / bottom / width / height, значения в пикселях или процентах.|"erid_position":"top:100px;right:100px;width:200px;"|
