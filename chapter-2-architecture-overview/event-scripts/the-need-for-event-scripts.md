### Применение Event-сценариев

Рассмотрим использование Event-сценариев по пунктам:

* Чаше всего они применяются для прослушивания событий от компонентов ввода. Например, как клик от Browser-Action или Page-Action, обработка нажатия горячих клавиш и событий выбранного пункта из контекстного меню. Более того, event-сценарий может прослушивать события адресатной строки браузера. Ниже наведён список компонентов и соответствующих событий.
  * chrome.browserAction - onClicked
  * chrome.pageAction - onClicked
  * chrome.commands - onCommand
  * chrome.contextMenus - onClicked
  * chrome.omnibox - onInputStarted, onInputChanged, onInputEntered, onInputCancelled

> **Примечание:**  
> onClicked событие не срабатывает, если компонент Browser-Action или Page-Action определены в манифесте.

* Другим важным аспектом использования это прослушивания событий создаваемых самим расширением. Вот некоторые из них: OnMessage, OnConnect, onInstalled, onUpdateAvailable, и т.д., которые принадлежат chrome.runtime объекту.

> **Примечание:**  
> Сценарии контента могут быть использованы для создания HTML-элементов на открытой веб-странице, которые относится к Content UI. Однако Content UI может выполнять, только стандартные события JavaScript. Кроме того, сценарий контента имеют ограниченный доступ к API Chrome Extensions, но имеют доступ к таким элементам как `chrome.runtime`, `chrome.extension`, и `chrome.storage`, а взаимодействие сценариев контента и сценариев расширения происходит при помощи обмена сообщений.

* Используя событие OnMessage \(или OnConnect\), event-сценарий может прослушивать сообщения из сценариев расширения. Кроме того, с помощью события`chrome.runtime.onMessageExternal`, сценарий может прослушивать сообщения непосредственно с веб-страницы.

* Помимо всех этих событий, event-сценарий может прослушивать события, которые связаны с вкладки, сообщениями, локальным хранилищем, историей, и т.д. Примеры таких событий перечислены ниже:

  * chrome.tabs - onCreated, OnUpdated, onRemoved, и т.п.
  * chrome.alarms - onAlarm
  * chrome.storage - OnChanged
  * chrome.bookmarks - onCreated, onRemoved, OnChanged, onImportBegan, onImportEnded, и т.п.
  * chrome.history - onVisited, onVisitRemoved

* Наиболее важным назначением является указания в этом сценарии событийных методов, так как они выполняется дольше, в отличие от Popup-сценария, которые запускается, только при открытии всплывающего окна. Event-сценарий автоматически загружаются, когда нужно выполнить метод события.

* Наконец, event-сценарии могут быть использованы для размещения логики расширения.


