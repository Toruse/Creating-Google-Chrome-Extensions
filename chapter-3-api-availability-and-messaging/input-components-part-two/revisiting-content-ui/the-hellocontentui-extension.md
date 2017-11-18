#### Расширение HelloContentUI

Данное расширение на основе указанного правила в атрибуте `matches`, подключает контент сценарий к веб странице example.org \(листинг 3-6\). Так же расширение использует Page-Action и Event сценарии \(Рисунок 3-12\). Само расширение на основе атрибута `permissions`и параметра `activeTab`, выполняется на активной вкладке.

![Рисунок 3-12. HelloContentUI: Фоновая страница](/assets/figure-3-12.png)

##### Рисунок 3-12. _HelloContentUI: Фоновая страница._

##### Листинг 3-6. _Chapter3/HelloContentUI/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "HelloContentUI",
    "description" : "Страница Page-Action с использованием Content-UI",
    "version" : "1.2",
    "page_action" : {
        "default_title" : "HelloContentUI",
        "default_icon" : "icon.png",
        "default_popup" : "popup.html"
    },
    "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : false
    },
    "permissions" : [
        "activeTab"
    ],
    "content_scripts" : [
        {
            "matches" : ["*://www.example.org/*"],
            "js" : ["content_script.js"]
        }
    ]
}
```

![Рисунок 3-13. HelloContentUI: Интеграция контент скрипта](/assets/figure-3-13.png)

##### Рисунок 3-13. _HelloContentUI: Интеграция контент скрипта._

##### Листинг 3-7. _Chapter3/HelloContentUI/content\_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World! - from content_script.js";
var requestMessage = {"data":"Test message X"};
var responseCallback = function(responseMessage) {
    console.log("responseMessage: " + responseMessage.data);
};
function createButton() {
    var button = document.createElement("button");
    button.style.width = "70px";
    button.style.height = "40px";
    button.style.position = "fixed";
    button.style.top = "10px";
    button.style.right = "10px";
    button.innerText = "Send Message";
    document.body.appendChild(button);
    return button;
}
//end-region

//region {вычисления}
console.log(consoleGreeting);
var button = createButton();
button.addEventListener("click",function() {
    console.log("Button clicked!");
    chrome.runtime.sendMessage(/*extensionId,*/requestMessage,responseCallback);
});
//end-region
```

Как показано на рисунке 3-13 контент сценарий \(content\_script.js\) используется для создания кнопки «Отправить сообщение». Метод `addEventListener `\(листинг 3-7\) используется для обработки клика на этой кнопке. Сама же кнопка указывает сценарию событий активировать Page-Action. Так как контент сценарий и сценарий событий - это различные компоненты, для взаимодействовать друг с другом используется механизм сообщений \(листинг 3-7 и 3-8\). Чтобы отправить такое сообщение в контент сценарии используется метод `runtime.sendMessage`.

##### Листинг 3-8. _Chapter3/HelloContentUI/event\_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World! - from event_script.js";
var responseMessage = {"data":"Test message Y"};
//end-region

//region {вычисления}
console.log(consoleGreeting);
//Показать Page-Action при помощи события onMessage
chrome.runtime.onMessage.addListener(function(requestMessage,sender,sendResponse) {
    chrome.pageAction.show(sender.tab.id);
    console.log("requestMessage: " + requestMessage.data);
    sendResponse(responseMessage);
});
//end-region
```



