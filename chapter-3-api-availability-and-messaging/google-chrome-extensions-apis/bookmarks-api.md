### Bookmarks API

API закладок \(`chrome.bookmarks`\) используется для создания, и управления закладками браузера. Для использования в файле манифеста нужно указать доступ `bookmarks`. Закладки организованы виде дерева, где каждый узел является закладкой или папкой. Сам узел это объект `bookmarks.BookmarkTreeNode`. 

Например, для создать закладки вызывается метод `chrome.bookmarks.create`, в который нужно передать идентификатор родителя, необязательный параметр заголовок и URL. Больше узнать о Bookmarks API можно по ссылке https://developer.chrome.com/extensions/bookmarks.

![Рисунок 3-33. Демонстрация API: Notifications API](/assets/figure-3-33.png)

##### Рисунок 3-33. _Демонстрация API: Notifications API._






