### Popup и Event сценарии

Теперь давайте посмотрим, как сценарий popup-окна взаимодействует с event-сценарием.

В расширении они выполняются в одной среде, но это два разными компонента. Соответственно должен присутствовать механизм общения между ними, и он на много проще предыдущих.

##### Листинг 3-20. _Chapter3/PSandES/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "Communication Demo: popup-script and event-script",
    "description" : "Показывает связь popup-сценария и event-сценария",
    "version" : "1.2",
    "browser_action" : {
        "default_title" : "Communication Demo: popup-script and event-script",
        "default_icon" : "icon.png",
        "default_popup" : "popup.html"
    },
    "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : false
    }
}
```

Так как используется popup-сценарий, то для всплывающего окна в файле манифесте нужно объявить параметр Browser-Action или Page-Action, как показано в листинге 3-20. Чтобы использовать event-сценарий \(листинг 3-22\) его нужно указать в атрибуте `background`.

##### Листинг 3-21. _Chapter3/PSandES/popup\_script.js_

```
//region {переменные и функции}
var sendMessageButtonID = "send_message";
var greeting = "Hello World!";
var message = "Test message X";
function responseCallback(responseObject) {
    console.log("Message '" + responseObject.message + "' from Sender '" + responseObject.sender + "'");
}
//end-region

//region {вычисления}
console.log(greeting);
document.addEventListener("DOMContentLoaded",function(dcle){
    var buttonID = document.getElementById(sendMessageButtonID);
    buttonID.addEventListener("click",function(ce) {
        //Это сообщение будет перехвачено в event_script.js
        chrome.runtime.sendMessage(message,responseCallback);
    });
});
//end-region
```

Отправка сообщения в event-сценарий выполняется вызовом метода chrome.runtime.sendMessage\(message,responseCallback\). Где параметр `message`– это сообщение для отправки, а `responseCallback`– функция обратного вызова, которая выполняется получателем сообщения.

В листинге 3-21 указан код popup-сценария расширения PSandES, а на рисунке 3-23 и 3-25 показан результат его работы.

![Рисунок 3-29. Демонстрация API: Downloads API](/assets/figure-3-29.png)

##### Рисунок 3-29. _Демонстрация API: Downloads API._

##### Листинг 3-22. _Chapter3/PSandES/event\_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var responseObject = {
    message : "Test message Y",
    sender : "event_script.js"
};
function GetFormattedMessageString(message,sender) {
    return "Message '" + message + "' from Sender '" + sender.url + "'";
}
//end-region

//region {вычисления}
console.log(greeting);
chrome.runtime.onMessage.addListener(function(message,sender,sendResponse) {
    sendResponse(responseObject); //Функция SendResponse будет вызываться в сценарии где определена
    console.log(GetFormattedMessageString(message,sender));
});
//end-region
```

Наконец, чтобы получить отправленное сообщение в event-сценарий, использует метод слушатель `chrome.runtime.onMessage`. Результат работы данного слушателя показан на рисунке 3-24. Обратите внимание выполняемая функция обратного вызова `SendResponse `и аргумент `responseObject `в event-сценарии инициализируется в popup-сценарии \(Рисунок 3-25\).

