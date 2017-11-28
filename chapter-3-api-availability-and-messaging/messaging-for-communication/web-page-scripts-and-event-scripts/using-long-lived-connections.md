#### Использование долгоживущих соединений

Мы рассмотрели обмен сообщениями один запрос один ответ. Иногда нужно производит передачу, которая длиться дольше. Для этих целей предназначен метод `chrome.runtime.connect`, который доступен в сценариях веб-страницы, контент сценария и Popup сценариях.

Данный метод первым параметром принимает `extensionID `- идентификатор расширения, которое подключается к долгоживущему соединению. Второй параметр объект, который содержит дополнительную информации о соединении, например: `{"name" : "connection1"}`. Сам метод возвращает объект `port`, а при помощи метода  `port.postMessage` происходит отправка сообщения.

> Примечание:
> Event-сценарий редко использует метод `chrome.runtime.connect`, и в основном вы будете встречать событийный метод `chrome.runtime.onConnect` или `chrome.runtime.onConnectExternal`. Они используются для общения с другими расширениями. Об этом можно почитать больше на [https://developer.chrome.com/extensions/messaging\#external](https://developer.chrome.com/extensions/messaging#external).

```
var port = chrome.runtime.connect("...",{"name" : "connection1"});
port.onMessage.addListener(function(message) {
    console.log(message);
});
port.postMessage("Test message X");
```



