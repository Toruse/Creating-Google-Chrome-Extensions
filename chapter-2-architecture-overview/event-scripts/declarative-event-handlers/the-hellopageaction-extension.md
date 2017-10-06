#### Расширение HelloPageAction

Как показано в листинге 2-6, кроме определения Page-Action, манифест содержит атрибут background. В дополнение к этому, появился новый атрибут permissions \(разрешение\), в котором прописан tabs. Данный параметр позволяет обращаться к вкладкам браузера и работать с ними.

##### Листинг 2-7. _Chapter2/HelloPageAction/event\_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World! - from event_script.js";
var queryInfoForAllTabs = {
    //"active":false,"currentWindow":true
};
function logTabs(tabs) {
    console.group("Tabs");
    console.log(tabs);
    console.groupEnd("Tabs");
}
function queryTabsAndShowPageActions() {
    chrome.tabs.query(
        queryInfoForAllTabs,
        function(tabs) {
            console.log("Количество вкладок: %s", tabs.length);
            logTabs(tabs); //Выводим объект tabs, визуально выделяя его в группу
            if(tabs.length > 0) {
                for(var i=0; i<tabs.length; i++) {
                    if(tabs[i].status === "complete") chrome.pageAction.show(tabs[i].id);
                }
            }
        }
    );
}
//end-region
```



