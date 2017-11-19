### API-интерфейс и события

Теперь приступим к изучению API для обмена сообщениями между различными типами сценариев. Данные сообщения работаю по принципу стандартного интерфейса JavaScript API на основе `window.postMessage`, и в рамках Extensions framework включают в себя соответствующие методы для отправки сообщений:

* `chrome.runtime.sendMessage`
* `chrome.runtime.connect` \(и соответствующий метод `port.postMessage`\)
* `chrome.tabs.sendMessage`
* `chrome.tabs.connect` \(и соответствующий метод `port.postMessage`\)

Чтобы прослушать сообщения используются следующие методы:

* `chrome.runtime.onMessage`
* `chrome.runtime.onMessageExternal`
* `chrome.runtime.onConnect` \(и соответствующий слушатель `port.onMessage`\)
* `chrome.runtime.onConnectExternal` \(и соответствующий слушатель `port.onMessage`\)





