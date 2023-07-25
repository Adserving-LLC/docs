# Adserving PostMessages

    Все события баннера отправляются через *postMessage*.  
    Для получения событий на уровне тега нужно разместить слушатель события `message` и разбирать их по типу.

## Существуют следующие типы событий:

### События показа
- Для **web** среды тип события: `ebInitAction` или `ebInitDone`;
- Для **In-App** среды события тип: `InAppImpression`.

```plain
Для возможности слушать события показа в In-App необходимо:
1. Исполенение в среде In-App и загрузка библиотеки MRAID.js;
2. Подсключения кастомного скрипта на стороне Adserving.
```

### События клика
Тип события: `ebclickthrough`, либо `ebUpdateClick`.

В качестве имени событий передается идентификатор кликовой:
1. Дефолтный клик: `_eyeblaster`
2. Все остальные имена относятся к доп. кликовым

### События схлопа/расхлопа
Тип события: `ebPanelAction`.

Имена событий:
1. Расхлоп: `ebPanelExpanded`
2. Схлоп: `ebPanelCollapsed`
3. Закрытие панели: `ebPanelClosed`


### Видео события
Тип события: `ebVideoInteraction`.

Имена основных событий:
1. Вкл/выкл звук: `ebVideoMute`, `ebVideoUnmute`
2. Состояние проигрывания: `ebVideoStarted`, `eb25Per_Played`, `eb50Per_Played`, `eb75Per_Played`, `ebVideoFullPlay`
3. Повторное проигрывание: `ebVideoReplay`

## Пример JS-кода для отслеживания событий креатива:

```js
window.addEventListener('message', function(e) {
  try {
    if ( e.data ) {
      var adserving_event = JSON.parse(e.data);
      if (adserving_event) {
        switch (adserving_event.type) {

          // Событие показа для web среды
          case 'ebInitAction':
          case 'ebInitDone'
            console.log('Adserving Impression');
            break;

          // Событие показа для in-App среды с использованием библиотеки MRAID.js
          case 'InAppImpression':
            console.log('Adserving In-App Impression');
            break;

          // События клика
          case 'ebclickthrough':
            console.log('Adserving Click Event:', adserving_event.data.intName);
            break;

          // События схлопа/расхлопа
          case 'ebPanelAction':
            console.log('Adserving Panel Event:', adserving_event.data.intName);
            break;

          // Видео события
          case 'ebVideoInteraction':
            console.log('Adserving Video Event:', adserving_event.data.intName);
            break;
        }
      }
    }
  } catch( err ) {}
});
```