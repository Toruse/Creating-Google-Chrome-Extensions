### Content и Event сценарии

Content сценарий не являются частью исполняемого расширения, но у него есть доступ к следующему API: `extension`, `i18n`, `runtime`, и `storage`. Так же данные скрипты имеют доступ к методам отправки сообщений `connect `и `sendMessage`.  

Так же обратите внимание, что сontent сценарии не имеет доступа к runtime.onMessageExternal и runtime.onConnectExternal, из-за это для взаимодействия с сценариями веб-страницы нужно использовать слушатели сообщений предусмотренные стандартными API JavaScript. 

Сперва мы познакомимся, как `content `сценарий может взаимодействовать со средой выполнения расширения, а в следующих разделах рассмотрим, как эти скрипты взаимодействуют с popup сценариями и сценариями веб-страницы.

С этой целью рассмотрим расширение CSandES  \(листинг 3-11, 3-12, 3-13\). Оно добавляет на основе правила манифеста `content_scripts.matches : "*://localhost/*"` \(листинг 3-13\) content сценарий на локальную веб-страницу. Сам код указан в листинге 3-11, а результат работы показан на рисунках 3-17 и 3-19.

![Рисунок 3-22. Проверка работы: консоль панель](/assets/figure-3-22.png)

##### Рисунок 3-22. _Проверка работы: консоль панель._

##### Листинг 3-11. _Chapter3/CSandES/content_script.js_

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
    /*
    //var port = chrome.runtime.connect("...",{"name":"connection1"});
    var port = chrome.runtime.connect({"name":"connection1"});
    port.onMessage.addListener(function(message){console.log(message);});
    port.postMessage("...");
    */
})();
//end-region
```
