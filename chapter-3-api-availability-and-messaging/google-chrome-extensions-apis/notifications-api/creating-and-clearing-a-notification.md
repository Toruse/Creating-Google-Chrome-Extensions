#### Создание и очистка уведомлений

Чтобы создать уведомление используется метод `chrome.notifications.create`, который принимает три параметра: `notificationId` \(строка\), `notificationOptions` \(объект\) и callback-функцию.

При помощи объекта `notificationOptions` описывается вид уведомления. Подробный список свойств можно посмотреть по ссылке [https://developer.chrome.com/apps/notifications\#type-NotificationOptions](https://developer.chrome.com/apps/notifications#type-NotificationOptions). Такие свойства как `title`, `message`, `buttons`, `imageUrl`, `items`, `progress` и др. определяют вид шаблона уведомления \(Рисунок 3-30-3-32\). Так же в листинге 3-27 обратите внимание на объект `NOTIFICATION_TEMPLATE_TYPE`, которая содержит список шаблонов уведомления.

Для скрытия уведомления используется метод `chrome.notifications.clear`, принимающий параметр  `notificationId`. Если нужно скрыть все уведомления, используется метод `chrome.notifications.getAll`, который передаёт в callback-функцию все уведомления виде объекта.

