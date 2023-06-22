# Adserving PostMessages

Все ивенты баннера отправляются через *postMessage*.  
На уровне тега нужно разместить слушатель события `message`, например:

```js
window.addEventListener('message', function(e) {
  try {
    if (e.data) {
      var sizmek_event = JSON.parse(e.data);
      if (sizmek_event) {
        switch (sizmek_event.type) {
          case 'ebInitAction':
            console.log('Sizmek Impression');
            break;
          case 'ebclickthrough':
            console.log('Sizmek Click Event:', sizmek_event.data.intName);
            break;
          case 'ebPanelAction':
            console.log('Sizmek Panel Event:', sizmek_event.data.intName);
            break;
          case 'ebVideoInteraction':
            console.log('Sizmek Video Event:', sizmek_event.data.intName);
            break;
        }
      }
    }
  } catch(err) {}
});
```

Событие показа для **web** среды имеет тип `ebInitAction`, либо `ebInitDone`.  
Для **In-App** этот тип событий говори о том, что креатив отрендерился.  
Для получения показа в In-App среде необходимо подписываться на событие `viewableChange` от MRAID.


События клика имеют тип `ebclickthrough`, либо `ebUpdateClick`. В качестве имени ивента передается идентификатор кликовой:
1. Дефолтный клик: `_eyeblaster`
2. Все остальные имена относятся к доп. кликовым


События схлопа/расхлопа имеют тип `ebPanelAction`. Имена ивентов:
1. Расхлоп: `ebPanelExpanded`
2. Схлоп: `ebPanelCollapsed`
3. Закрытие панели: `ebPanelClosed`


События, относящиеся к видео имеют тип **ebVideoInteraction**. Имена основных ивентов:
1. Вкл/выкл звук: `ebVideoMute`, `ebVideoUnmute`
2. Состояние проигрывания: `ebVideoStarted`, `eb25Per_Played`, `eb50Per_Played`, `eb75Per_Played`, `ebVideoFullPlay`
3. Повторное проигрывание: `ebVideoReplay`
