#### Использование долгоживущих соединений

Мы рассмотрели обмен сообщениями один запрос один ответ. Иногда нужно производит передачу, которая длиться дольше. Для этих целей предназначен метод `chrome.runtime.connect`, который доступен в сценариях веб-страницы, контент сценария и Popup сценариях.

Данный метод первым параметром принимает `extensionID`- идентификатор расширения, которое подключается к долгоживущему соединению. Второй параметр объект, который содержит дополнительную информации о соединении, например: `{"name" : "connection1"}`. Сам метод возвращает объект `port`, а при помощи метода  `port.postMessage` происходит отправка сообщения.

```
var port = chrome.runtime.connect("...",{"name" : "connection1"});
port.onMessage.addListener(function(message) {
    console.log(message);
});
port.postMessage("Test message X");
```

> Примечание:  
> Event-сценарий редко использует метод `chrome.runtime.connect`, и в основном вы будете встречать событийный метод `chrome.runtime.onConnect` или `chrome.runtime.onConnectExternal`. Об этом можно почитать больше на [https://developer.chrome.com/extensions/messaging\#external](https://developer.chrome.com/extensions/messaging#external).

Чтобы принять сообщение, используется перехватчик `chrome.runtime.onConnectExternal`, в который передается объект `port`. И наконец, чтобы слушать входящие сообщения, назначаем`port.onMessage`. В результате оба скрипта имеют доступ к общему порту, и могу одновременно прослушивать сообщения. Как показано  в коде ниже:

```
chrome.runtime.onConnectExternal.addListener(function(port) {
    //if(port.name == "connection1")
    port.onMessage.addListener(function(message) {
        console.log(message); //Test message X
        port.postMessage("Test message Y");
    });
});
```

![Рисунок 3-21. Проверка работы: консоль панель](/assets/figure-3-21.png)

##### Рисунок 3-21. _Проверка работы: консоль панель._



