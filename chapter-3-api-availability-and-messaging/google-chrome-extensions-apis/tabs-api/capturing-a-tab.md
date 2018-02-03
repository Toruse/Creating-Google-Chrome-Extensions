#### Захват вкладки

Для того, чтобы захватить видимую область активной вкладки используется метод `chrome.tabs.captureVisibleTab`. Он принимает три параметра `windowId`, `options` и `callbackWindowID`. `WindowID` параметр не обязательный, и по умолчанию имеет значение текущего окна. Параметр `options` используется для указания формата изображения. Третий параметр callback-функция принимает `dataUrl` \(тип строка\) в котором находиться URL-адрес на данные содержащие закодированное изображение захваченной части вкладки. Обратите внимание, что данные из `dataUrl` могут быть переданы свойству `src` элемента `IMG`, как показано в листинге 3-29. Результат работы показан на рисунке 3-36. Также этот метод для работы требует доступ `<all_urls>` в файле манифеста \(Листинге 3-30\).
