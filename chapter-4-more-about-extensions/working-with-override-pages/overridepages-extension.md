### Расширение OverridePages

Расширение OverridePages переопределяет новую вкладку \(Рисунок 4-2\). Обратите внимание на подсказку, которая появляется при загрузке данного расширения \(Рисунок 4-1\). Это браузер Chrome спрашивает подтверждение на переопределение страницы.

Подключаемый сценарий myNewTab\_1.js \(Листинг 4-5, 4-6\) создает список из закладок браузера, которые добавляются в `<ul id="list"></ul>` список HTML-страницы указанной в листинге 4-4.

![Рисунок 4-4. Страница настроек в стиле Google Chrome](/assets/figure-4-4.png)

##### Рисунок 4-4. _Страница настроек в стиле Google Chrome._

##### Листинг 4-5. _Chapter4/OverridePages/myNewTab\_1.js_

```
//region {переменные и функции}
var folders = [];
var listName = "list";
var host = "developer.chrome.com";
var itemBorderRightStyle = "5px solid #666";
var itemBoxShadowStyle = "0px 0px 2px #333";
var itemBackgroundColor = "#ccc";
var storageKey = "APPEND_MATCHING_ONLY";
function appendItem(listElement,nodeURL,nodeParentTitle) {
    var li = document.createElement("li");
    var a = document.createElement("a");
    a.href = nodeURL;
    a.innerText = nodeURL + " (" + nodeParentTitle + ")";
    li.appendChild(a);
    if(nodeURL.indexOf(host) != -1) {
        li.style.borderRight = itemBorderRightStyle;
        li.style.boxShadow = itemBoxShadowStyle;
        li.style.backgroundColor = itemBackgroundColor;
    }
    listElement.appendChild(li);
}
function appendMatchingItem(listElement,nodeURL,nodeParentTitle) {
    if(nodeURL.indexOf(host) != -1) appendItem(listElement,nodeURL,nodeParentTitle);
}
function populateList(listElement) {
    folders.forEach(function(folder) {
        folder.children.forEach(function(bookmarkTreeNode) {
            appendItem(listElement,bookmarkTreeNode.url,folder.title);
        });
    });
}
function populateListV2(listElement) {
    chrome.storage.sync.get(storageKey,function(items) {
        if(!chrome.runtime.lastError && items[storageKey]) {
            olders.forEach(function(folder) {
                folder.children.forEach(function(bookmarkTreeNode) {
                    if(bookmarkTreeNode.url)
                        appendMatchingItem(listElement,bookmarkTreeNode.url,folder.title);
                    });
                });
        } else {
            folders.forEach(function(folder) {
                folder.children.forEach(function(bookmarkTreeNode) {
                    if(bookmarkTreeNode.url)
                        appendItem(listElement,bookmarkTreeNode.url,folder.title);
                });
            });
        }
    });
}
//end-region
```

Для отображения закладок на новой вкладке используется API `chrome.bookmarks`. Чтобы получить дерево закладок используется метод `chrome.bookmarks.getTree`, а для работы с элементами используется объект `bookmarks.BookmarkTreeNode`.

В листинге 4-6 для доступа к вложенным закладкам используется свойство `children.length`. Все полученные закладки сохраняются в массив `folder`.

В листинге 4-5 показаны функции `populateList` и `populateListV2`, которые на основе `folder` создают список закладок для добавления в HTML переопределяемой страницы.

![Рисунок 4-5. Страница настроек: вывод логов в консоль](/assets/figure-4-5.png)

##### Рисунок 4-5. _Страница настроек: вывод логов в консоль._

##### Листинг 4-6. _Chapter4/OverridePages/ myNewTab\_1.js_

```
//region {вычисления}
document.addEventListener("DOMContentLoaded",function(dcle) {
    var listElement = document.getElementById(listName);
    chrome.bookmarks.getTree(function(bookmarkTreeAsArray) {
        var bookmarkTree = bookmarkTreeAsArray[0];
        if(bookmarkTree.children) {
            bookmarkTree.children.forEach(function(node) {
                if(node.children.length > 0) folders.push(node);
            });
        }
        //populateList(listElement);
        populateListV2(listElement);
    });
});
//end-region
```



