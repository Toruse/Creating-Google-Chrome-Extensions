### Скрипты веб-страницы и Event-сценарии

Основная идея данного расширения – это чтобы внешняя веб-страница связалась с ним.

В браузере Chrome, страницы \(кроме страницы Менеджера расширений\) имеют доступ к методу отправки сообщений chrome.runtime.sendMessage \(листинг 3-9\), который принимает следующие параметры:

* `extensionID`
* `message`
* `responseCallback`

Параметр `extensionID`- это идентификатор расширения. Его можно посмотреть на странице Менеджер расширений \(Рисунок 3-16\). Данный идентификатор не постоянный и меняется при загрузке или правках содержимого расширения.

> **Примечание:**  
> Чтобы с эмулировать реальную работу сайта, для расширения WSandES использовался локальный веб-сервер. Обратите внимание, что основной файл имеет суффикс .php, который содержит простую HTML разметку. Соответственно, его можно открыть непосредственно в браузере Chrome.

##### 

##### 

##### Листинг 3-9. _Chapter3/WSandES/WebServer/webpage\_script.js_

```
//region {переменные и функции}
//Внимание! Значение данной переменной смотрите на странице Расширений
var extensionID = "aafejdaofaaaedckjdhoeigbopfeooem";
var sendMessageButtonID = "send_message";
var greeting = "Hello World!";
var message = "Test message X";
function responseCallback(responseObject) {
    console.log("Message '" + responseObject.message + "' from Sender '" + responseObject.sender + "'");
}
//end-region

//region {вычисления}
console.log(greeting);
document.addEventListener("DOMContentLoaded",function(dcle) {
    var buttonID = document.getElementById(sendMessageButtonID);
    buttonID.addEventListener("click",function(ce) {
        //Это сообщение будет перехвачено сценарием event_script.js
        chrome.runtime.sendMessage(extensionID,message,responseCallback);
    });
});
//end-region
```

Параметр `message `метода `sendMessage `содержит сроковое сообщение для отправки, и имеет значение «Test message X».

Параметр `responseCallback `является функцией обратного вызова, которая запускается в среде расширения, но выполняется в контексте сценария веб-страницы \(листинге 3-9 и 3-10\). Результат работы расширения показано на рисунке 3-15.



