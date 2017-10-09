##### Добавление и удаление правил

Если вы желаете задекларировать правила для события onPageChanged, то используйте chrome.declarativeContent.onPageChanged.\*. Где \* может означать addRules или removeRules. Метод addRules принимает массив правил и callback-функцию.

```
var rule1 = {
    id : "some_rule_A", //Если не установлено свойство, оно будет создано
    priority : 100, //Опция, значение по умолчанию 100
    conditions : [/*условия*/],
    actions : [/*действия*/]
};
...
var ruleList = [rule1,rule2,...];
chrome.declarativeContent.onPageChanged.addRules(ruleList);
```

Для удаления правил используется метод removeRules. Он принимает массив с идентификаторами правил \(например, \[rule1.id, rule2.id\] \) в качестве первого параметра и функцию обработки в качестве второго параметра. Если массив не определён, то будут удалены все зарегистрированные правила.

##### Листинг 2-9. _Chapter2/PageActionNotes/event\_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World! - from event_script.js";
var ruleStackOverflowHost = {
    "conditions" : [
        new chrome.declarativeContent.PageStateMatcher({
            "pageUrl" : {
                "hostEquals" : "stackoverflow.com",
                "schemes" : ["http","https"]
            }
        })
    ],
    "actions" : [new chrome.declarativeContent.ShowPageAction()]
};
//end-region
```

> **Примечание:**
> Правила добавляются во время установки расширения, при помощи события runtime.onInstalled. Однако, это событие также срабатывает, когда выполняется обновление расширения. Соответственно, вы должны сначала удалить ранее установленные правила, а затем зарегистрировать новые правила. 

##### Листинг 2-10. _Chapter2/PageActionNotes/event\_script.js_

```
//region {вызов}
console.log(consoleGreeting);
chrome.runtime.onInstalled.addListener(function() {
    //Удаляем и заменяем правила
    chrome.declarativeContent.onPageChanged.removeRules(undefined,function() {
        //Указываем новые правила
        chrome.declarativeContent.onPageChanged.addRules([ruleStackOverflowHost]);
    });
});
//end-region
```



