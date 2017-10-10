##### Использование ShowPageAction

В предыдущем разделе, было показано, как отобразить Page-Action страницу при помощи `chrome.tabs.query` и `chrome.tabs.onUpdated` события. Теперь рассмотрим ещё один способ, как это сделать с помощью декларированного обработчика событий.

> **Примечание:**  
> Чтобы подробней ознакомиться с данной темой советуем посетить страницу [https://developer.chrome.com/extensions/declarativeContent](https://developer.chrome.com/extensions/declarativeContent).

Как показано в листинге 2-9, в объекте правил `ruleStackOverflowHost `указано условие и действие. Условие представлено объектом PageStateMatcher, который проверяет соответствие веб-страницы указанным правилам. В листинге 2-9 указанные критерии` pageUrl.hostEquals` и `pageUrl.schemes`, что соответствует веб-ресурсу stackoverflow.com. Кроме свойства `pageUrl `можно указать `css`. Рассмотрим пример, отображения Page-Action страницы на ресурсе [https://www.google.com/](https://www.google.com/) с наличием поля для ввода пароля:

