## API расширения Google Chrome

Расширения Google Chrome имеют доступ к различным API, которые дают доступ почти ко всем функция браузера. Некоторое API уже рассматривались в предыдущих главах – это `chrome.omnibox`, `chrome.contextMenus`, `chrome.commands`,`chrome.pageAction` и `chrome.browserAction`.

В этом разделе будут разморены следующие API:

* alarms
* bookmarks
* downloads
* history
* notifications
* storage
* tabs

> **Примечание:**  
> Так же расширения могут использовать стандартный JavaScript API, это самое ядро JavaScript, Document Object Model \(DOM\), XMLHttpRequest \(XHR\), HTML5, WebKit, CSS-анимацию, JSON, а также API V8.

В дополнение к указанным API будет рассмотрено XHR API, который входит в стандартный API JavaScript. Ещё есть много других API компонентов, но они не будут рассматриваться в данной книге, а узнать про низ можно по ссылке [https://developer.chrome.com/extensions/api\_index](https://developer.chrome.com/extensions/api_index). Вот некоторые из них:

* contentSettings
* cookies
* desktopCapture
* extension
* management
* system.cpu
* system.memory
* webstore
* windows



