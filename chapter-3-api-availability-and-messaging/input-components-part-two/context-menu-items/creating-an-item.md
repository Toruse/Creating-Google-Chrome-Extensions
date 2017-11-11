#### Создание элемента

Существуют различные типы пунктов контекстного меню, основные – это стандартный \(`normal`\), разделитель \(`separator`\), и флажок \(`checkbox`\). В нашем расширении мы создадим стандартный пункт меню.

![Рисунок 3-9. HelloContextMenuItem: Фоновая страница](/assets/figure-3-9.png)

##### Рисунок 3-9. _HelloContextMenuItem: Фоновая страница._

Каждый пункт контекстного меню имеет уникальный идентификатор. В листинге 3-4 для этого определяется переменная `ID_CONTEXT_MENU_ITEM_HELLO`. Далее указан список типов элементов меню. В нашем случае будет указан стандартный \(`normal`\) тип. Чтобы указать на каком элементе страницы применять пункт меню, нужно указать параметр `contexts`. Соответственно в переменной `TYPES_CONTEXT` перечислены поддерживаемые элементы контекста. Так как меню нашего расширения должно взаимодействовать с выделенным содержимым, нужно указать значение `selection`.

##### Листинг 3-4. _Chapter3/HelloContextMenuItem/event_script.js_

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
    //"targetUrlPatterns" используется для TYPES_CONTEXT.IMAGE, TYPES_CONTEXT.VIDEO, TYPES_CONTEXT.AUDIO, etc.
    "targetUrlPatterns" : []
};
//end-region
```

