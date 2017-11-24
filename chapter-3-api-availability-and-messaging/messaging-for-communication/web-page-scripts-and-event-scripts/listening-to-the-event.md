#### Прослушивание события

Как показано в листинге 3-10, для обработки сообщения от внешней веб-страницы используется метод `chrome.runtime.onMessageExternal`, который передает три параметра: `message`, `sender`, и `sendResponse`. Параметр `sendResponse `содержит функцию обработчик, которая запускается на выполнение в контексте сценария веб-страницы.

##### Листинг 3-10. _Chapter3/WSandES/event_script.js_

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







