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

В листинг 2-7 и 2-8 показан основной код расширения. Как видно функция queryTabsAndShowPageAction использует метод chrome.tabs.query \(данный метод возвращает массив вкладок\), в который передается первый параметр объект queryInfoForAllTabs. В данном примере он пуст, соответственно вернуться все вкладки.

Второй аргумент метода представляет собой функцию callback, в которую передается выбраный массив вкладок. В рамках расширения Chrome, каждая вкладка представлена собой объект типа tabs.

Для того чтобы отобразить Page-Action страницу нам понадобиться метод chrome.pageAction.show и параметр id вкладки. Таким образом цикл for\(var i=0; i&lt;tabs.length; i++\) перебирает все вкладки и подключает возможность отобразить Page-Action страницу.

##### Листинг 2-8. _Chapter2/HelloPageAction/event\_script.js_

```
//region {calls}
console.log(consoleGreeting);
//Show Page-Actions using the chrome.tabs.query method
//queryTabsAndShowPageActions();
//Show Page-Actions using the onUpdated event
chrome.tabs.onUpdated.addListener(function(tabId,changeInfo,tab) {
    chrome.pageAction.show(tabId);
});
//end-region
```

Однако, есть один недостаток, использования функции queryTabsAndShowPageActions, она выполняется один раз при загрузке браузера. Если вы, например, откроете новую вкладку, страница Page-Action не будет отображаться. В данной ситуации для вкладки нужно повесить слушатель OnUpdated \(см. листинг 2-8\). Далее функцию queryTabsAndShowPageActions нужно закомментировать, а в OnUpdated указать метод chrome.pageAction.show, в который передаётся идентификатор вкладки tabId. Таким образом, каждый раз, когда вкладка открывается или обновляется слушатель отобразит Page-Action страницу на соответствующей вкладке.

