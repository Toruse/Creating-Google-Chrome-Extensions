### Применение Event-сценариев

Рассмотрим использование Event сценариев по пунктам:

* Чаше всего они применяются для прослушивания событий от компонентов ввода. Например, как клик от Browser-Action или Page-Action, обработка нажатия горячих клавиш и события выбранного пункта из контекстного меню. Более того, event-сценарий может прослушивать события адресатной строки браузера. Ниже наведён список компонентов и соответствующих событий.
     * chrome.browserAction - onClicked
     * chrome.pageAction - onClicked
     * chrome.commands - по команде
     * chrome.contextMenus - onClicked
     * chrome.omnibox - onInputStarted, onInputChanged, onInputEntered, onInputCancelled

> **Примечание:**
> onClicked событие не срабатывает, если компонент Browser-Action или Page-Action определены в манифесте.

* Другим важным аспектом использования это прослушивания событий, создаваемых самим расширением. Это OnMessage, OnConnect, onInstalled, onUpdateAvailable, и т.д., которые доступны в chrome.runtime объекте.



