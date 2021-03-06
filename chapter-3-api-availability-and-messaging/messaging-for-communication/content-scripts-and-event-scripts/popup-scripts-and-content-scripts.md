#### Popup и Content скрипты

Теперь давайте рассмотрим на примере расширения PSandCS, как сценарии всплывающего окна взаимодействует с content сценариями. Код указан в листинге 3-14 и 3-16. Результат работы показан на рисунках 3-20 и 3-21.

Исходя из файла манифеста \(Листинг 3-14\), расширение добавляет content-скрипт на посещаемую веб-страницу example.org. Так же указан атрибут`browser_action`, для подключения всплывающего окна, которое содержит элемент “Send Message” с идентификатором `send_message` \(Рисунок 3-21\). Далее к элементу `send_message` прикрепляется событие на клик \(Листинг 3-15\).

##### Листинг 3-14. _Chapter3/PSandCS/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "Communication Demo: popup-script and content-script",
    "description" : "Показывает связь popup-сценария и content-сценария",
    "version" : "1.2",
    "content_scripts" : [
        {
            "matches" : ["*://www.example.org/*"],
            "js" : ["content_script.js"]
        }
    ],
    "browser_action" : {
        "default_title" : "Communication Demo: popup-script and content-script",
        "default_icon" : "icon.png",
        "default_popup" : "popup.html"
    }
}
```

В листинге 3-15, для получения активной вкладки использование метода `chrome.tabs.query`. Чтобы отправить сообщение из content-скрипта используется метод `chrome.tabs.sendMessage`, который принимает следующие параметры.

* `tabID`
* `message`
* `responseCallback`

`tabID`- это идентификатор вкладки, которая отправляет сообщение. Параметр `message`– это отправляемое сообщение, и в нашем случае содержит строку “Test message X”. Параметр `responseCallback`является функцией обратного вызова.

![Рисунок 3-25. Расширение PSandES: Инспектирование Popup-окна](/assets/figure-3-25.png)

##### Рисунок 3-25. _Расширение PSandES: Инспектирование Popup-окна._

##### Листинг 3-15. _Chapter3/PSandCS/popup\_script.js_

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
        chrome.tabs.query({"active":true},function(tabs) {
            chrome.tabs.sendMessage(tabs[0].id,message,responseCallback);
        });
    });
});
//end-region
```

Content сценарий содержит код для перехвата отправленного сообщения при помощи метода `chrome.runtime.onMessag`. Далее \(листинг 3-16\), полученное сообщение с помощью `console.log` выводиться в консоль \(Рисунке 3-20\). Обратите внимание, что добавляемая кнопка на веб-страницу не используется.

##### Листинг 3-16. _Chapter3/PSandCS/content_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World!";
var responseObject = {
    message : "Test message Y",
    sender : "content_script.js"
};
function GetFormattedMessageString(message,sender) {
    return "Message '" + message + "' from Sender '" + sender.id + "'";
}
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
chrome.runtime.onMessage.addListener(function(message,sender,sendResponse) {
    sendResponse(responseObject); //SendResponse будет вызываться там где определена в сценарии
    console.log(GetFormattedMessageString(message,sender));
});
//end-region
```


