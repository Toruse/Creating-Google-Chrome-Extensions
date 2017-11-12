#### Создание элемента

Существуют различные типы пунктов контекстного меню, основные – это стандартный \(`normal`\), разделитель \(`separator`\), и флажок \(`checkbox`\). В нашем расширении мы создадим стандартный пункт меню.

![Рисунок 3-9. HelloContextMenuItem: Фоновая страница](/assets/figure-3-9.png)

##### Рисунок 3-9. _HelloContextMenuItem: Фоновая страница._

Каждый пункт контекстного меню имеет уникальный идентификатор. В листинге 3-4 для этого определяется переменная `ID_CONTEXT_MENU_ITEM_HELLO`. Далее указан список типов элементов меню. В нашем случае будет указан стандартный \(`normal`\) тип. Чтобы указать на каком элементе страницы применять пункт меню, нужно указать параметр `contexts`. Соответственно в переменной `TYPES_CONTEXT` перечислены поддерживаемые элементы контекста. Так как меню нашего расширения должно взаимодействовать с выделенным содержимым, нужно указать значение `selection`.

##### Листинг 3-4. _Chapter3/HelloContextMenuItem/event\_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World! - from event_script.js";
function logSuccess(task) {console.log("%s Successful!",task);}
function logFailure(task) {console.log("%s Failed!",task);}
var ID_CONTEXT_MENU_ITEM_HELLO = "ID_CONTEXT_MENU_ITEM_HELLO";
var TYPES_CONTEXT_MENU_ITEM = {
    "NORMAL" : "normal",
    "CHECKBOX" : "checkbox",
    "RADIO" : "radio",
    "SEPARATOR" : "separator"
};
var TYPES_CONTEXT = {
    "ALL" : "all",
    "PAGE" : "page",
    "FRAME" : "frame",
    "SELECTION" : "selection",
    "LINK" : "link",
    "EDITABLE" : "editable",
    "IMAGE" : "image",
    "VIDEO" : "video",
    "AUDIO" : "audio",
    "LAUNCHER" : "launcher",
    "BROWSER_ACTION" : "browser_action",
    "PAGE_ACTION" : "page_action"
};
var match_pattern_stackoverflow = "*://*.stackoverflow.com/*";
var createProperties = {
    "type" : TYPES_CONTEXT_MENU_ITEM.NORMAL,
    "id" : ID_CONTEXT_MENU_ITEM_HELLO,
    "title" : "Custom search '%s'",
    "contexts" : [TYPES_CONTEXT.ALL],
    "documentUrlPatterns" : [match_pattern_stackoverflow],
    //"targetUrlPatterns" используется для TYPES_CONTEXT.IMAGE, TYPES_CONTEXT.VIDEO, TYPES_CONTEXT.AUDIO, etc.
    "targetUrlPatterns" : []
};
//end-region
```

Код расширения HelloContextMenuItem показан в листингах 3-4 и 3-5. Он добавляет пункт меню на посещаемую веб-страницу \(Рисунок 3-10\). Если есть желание, чтобы меню добавлялось, например, на сайте stackoverflow.com, то нужно задать шаблон в свойстве `documentUrlPatterns`. В листинге 3-4 шаблон указан в переменной `match_pattern_stackoverflow`, который передается в объект `createProperties`, он же в свою очередь используется для создания пункта меню.

![Рисунок 3-10. HelloContextMenuItem: Компонент пункта контекстного меню](/assets/figure-3-10.png)

##### Рисунок 3-10. _HelloContextMenuItem: Компонент пункта контекстного меню._

##### Листинг 3-5. _Chapter3/HelloContextMenuItem/event\_script.js_

```
//region {вызовы}
console.log(consoleGreeting);
chrome.contextMenus.create(createProperties,function() {
    if(!chrome.runtime.lastError) {
        logSuccess("ContextMenus.Create");
        chrome.contextMenus.onClicked.addListener(function(info,tab) {
            console.log("id: %s, selection: %s, url: %s",info.menuItemId,info.selectionText,tab.url);
        });
    } else {
        logFailure("ContextMenus.Create");
    }
});
//end-region
```

Создание пункта контекстного меню происходит в два этапа. Первый, это создание самого пункта \(Рисунок 3-9\), а второй назначение слушателя `onClicked`. Создание пункта контекстного меню осуществляется при помощи метода `contextMenus.create`, который принимает в качестве первого параметра объект с заданными свойствами. Если при создании возникнет ошибка, то объект`chrome.runtime.lastError` вернёт её. И наоборот, если создание прошло успешно, вы можете назначить слушатель `onClicked`\(Листинг 3-5\).

![Рисунок 3-11. HelloContextMenuItem: Фоновая страница](/assets/figure-3-11.png)

##### Рисунок 3-11. _HelloContextMenuItem: Фоновая страница._

В процессе работы, слушатель получает объект `info `и объект `tab`. Объект `info `содержит информацию о нажатом пункте меню, которую можно использовать для определения какие действия нужно выполнить. Например: в листинге 3-5 свойство `info.menuItemId` содержит идентификатор меню, которое просто выводиться в консоль \(Рисунок 3-11\).

Ознакомится со всем списком свойств объекта info можно по адресу https://developer.chrome.com/extensions/contextMenus.

