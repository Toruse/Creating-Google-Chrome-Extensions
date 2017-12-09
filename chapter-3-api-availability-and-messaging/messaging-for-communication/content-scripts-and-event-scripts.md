### Content и Event сценарии

Content сценарий не являются частью исполняемого расширения, но у него есть доступ к следующему API: `extension`, `i18n`, `runtime`, и `storage`. Так же данные скрипты имеют доступ к методам отправки сообщений `connect`и `sendMessage`.

Так же обратите внимание, что сontent сценарии не имеет доступа к runtime.onMessageExternal и runtime.onConnectExternal, из-за это для взаимодействия с сценариями веб-страницы нужно использовать слушатели сообщений предусмотренные стандартными API JavaScript.

Сперва мы познакомимся, как `content`сценарий может взаимодействовать со средой выполнения расширения, а в следующих разделах рассмотрим, как эти скрипты взаимодействуют с popup сценариями и сценариями веб-страницы.

С этой целью рассмотрим расширение CSandES  \(листинг 3-11, 3-12, 3-13\). Оно добавляет на основе правила манифеста `content_scripts.matches : "*://localhost/*"` \(листинг 3-13\) content сценарий на локальную веб-страницу. Сам код указан в листинге 3-11, а результат работы показан на рисунках 3-17 и 3-19.

![Рисунок 3-22. Проверка работы: консоль панель](/assets/figure-3-22.png)

##### Рисунок 3-22. _Проверка работы: консоль панель._

##### Листинг 3-11. _Chapter3/CSandES/content\_script.js_

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

Как показано в листинге 3-11, после подключения скрипта к веб-странице, он добавит кнопку на которую прикрепит событие отправляющее сообщение при помощи метода `chrome.runtime.sendMessage`. Так как параметр `extensionID`не обязательный в данном примере он не указывается.

##### Листинг 3-12. _Chapter3/CSandES/event\_script.js_

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
    sendResponse(responseObject); //SendResponse будет выполнен в том скрипте, где определён
    console.log(GetFormattedMessageString(message,sender));
});
//end-region
```

![Рисунок 3-23. Расширение PSandES: Инспекция popup окна](/assets/figure-3-23.png)

##### Рисунок 3-23. _Расширение PSandES: Инспекция popup окна._

В листинге 3-12 указан код event сценария. Поскольку обмен сообщениями выполняется в пределах расширения, то по сравнению с предыдущим примером \(листинг 3-10\), вместо слушатель `onMessageExternal`используется `onMessage`. Если нужно установить постоянное соединение, то потребуется функция слушатель для `chrome.runtime.onConnect`. Указанный вариант находиться в комментариях листинга 3-12. На рисунке 3-18 показан результат работы расширения.

##### Листинг 3-13. _Chapter3/CSandES/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "Communication Demo: content-script and event-script",
    "description" : "Показывает связь content-скрипта и event-сценария",
    "version" : "1.2",
    "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : false
    },
    "content_scripts" : [
        {
            "matches" : ["*://localhost/*"],
            "js" : ["content_script.js"]
        }
    ]
}
```

![Рисунок 3-24. Консольная панель фоновой страницы](/assets/figure-3-24.png)

##### Рисунок 3-24. _Консольная панель фоновой страницы._



