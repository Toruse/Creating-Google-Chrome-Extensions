#### Создание закладок

Чтобы создать закладку, используется метод `chrome.bookmarks.create`, который принимает два параметра `bookmark`\(объект\) и `callback` \(функция\). В свою очередь объект `bookmark` содержит: `parentId`, `title`, и `url`. Если в параметре `url` задана пустая строка или ноль, то будет создана папка. После чего выполниться `сallback` функция, в которую будет передан аргумент типа `BookmarkTreeNode`.

![Рисунок 3-34. Демонстрация API: Notifications API](/assets/figure-3-34.png)

##### Рисунок 3-34. _Демонстрация API: Notifications API._

Листинг 3-24 содержит фрагмент кода, в котором на основе объекта Bookmark1 создается папка, а затем callback функция на основе `result.id` создает в ней закладку \(Рисунок 3-27\). Чтобы получить созданную закладку можно использовать метод `chrome.bookmarks.get`, которая принимает идентификатор закладки или массив идентификаторов \(Листинге 3-24\), а результат обрабатывает callback-функцией принимающая массив найденных объектов BookmarkTreeNode.

##### Листинг 3-24. _Chapter3/BookmarksAPI/event_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var bookmark1 = {
    title : "MyBookmark1",
    //Если URL является пустым или отсутствует, создана закладка будет папкой
    url : ""
};
var bookmark2 = {
    title : "MyBookmark2",
    url : "http://www.example.org"
};
var queryObject = {
    query : "",
    url : "",
    title : "chrome extensions"
};
var queryString = "example url";
//end-region

//region {вычисления}
console.log(greeting);

/*
//result имеет тип BookmarkTreeNode
chrome.bookmarks.create(bookmark1,function(result) { 
    console.log("Created bookmark with id: " + result.id);
    bookmark2.parentId = result.id;
    chrome.bookmarks.create(bookmark2);
});
*/

/*
//id закладки (тип строка) или массив id закладок (тип строка)
chrome.bookmarks.get("1234",function(results) { 
    console.log(results); //массив BookmarkTreeNode
});
*/

/*
//поддерживает только название и url
chrome.bookmarks.update("6",{"title":"Example URL"}); 
*/

chrome.bookmarks.search(queryString,function(results) { //string or object query
    console.log(results); //массив BookmarkTreeNode
});
//end-region
```


