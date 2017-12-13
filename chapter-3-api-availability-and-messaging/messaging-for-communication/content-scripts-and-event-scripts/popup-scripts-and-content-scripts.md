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

`tabID `- это идентификатор вкладки, которая отправляет сообщение. Параметр `message `– это отправляемое сообщение, и в нашем случае содержит строку “Test message X”. Параметр `responseCallback `является функцией обратного вызова.

![Рисунок 3-25. Расширение PSandES: Инспектирование Popup-окна](/assets/figure-3-25.png)

##### Рисунок 3-25. _Расширение PSandES: Инспектирование Popup-окна._

##### Листинг 3-15. _Chapter3/PSandCS/ popup_script.js_

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
(function(){
    var buttonElement = document.createElement("button");
    buttonElement.style.position = "fixed";
    buttonElement.style.display = "block";
    buttonElement.style.width = "70px";
    buttonElement.style.height = "40px";
    buttonElement.style.bottom = "10px";
    buttonElement.style.left = "10px";
    buttonElement.innerText = "Message Runtime";
    buttonElement.addEventListener("click",function(ce) {
        //Это сообщение будет перехвачено в event_script.js
        chrome.runtime.sendMessage(message,responseCallback);
    });
    document.body.appendChild(buttonElement);
})();
//end-region
```

