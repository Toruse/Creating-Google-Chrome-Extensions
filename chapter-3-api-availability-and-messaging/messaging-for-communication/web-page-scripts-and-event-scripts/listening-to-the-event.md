#### Прослушивание события

Как показано в листинге 3-10, для обработки сообщения от внешней веб-страницы используется метод `chrome.runtime.onMessageExternal`, который передает три параметра: `message`, `sender`, и `sendResponse`. Параметр `sendResponse `содержит функцию обработчик, которая запускается на выполнение в контексте сценария веб-страницы.

##### Листинг 3-10. _Chapter3/WSandES/event_script.js_

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
chrome.runtime.onMessageExternal.addListener(function(message,sender,sendResponse) {
    sendResponse(responseObject); //Будет вызван из сценария, где определён sendResponse
    console.log(GetFormattedMessageString(message,sender));
});
//end-region
```







