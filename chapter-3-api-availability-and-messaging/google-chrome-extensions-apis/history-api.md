### History API

History API \(`chrome.history`\) используется для работы со списком посещенных страниц. Так же, есть возможность добавлять, удалять и запрашивать URL-адреса из истории браузера. Листинг 3-26 содержит пример использования HistoryAPI.

##### Листинг 3-26. _Chapter3/HistoryAPI/event\_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var tenMinutesAsMilliseconds = 10 * 60 * 1000;
//getTime возвращает количество миллисекунд, прошедших с полуночи 1 января 1970 года GMT
var currentTimeAsMilliseconds = new Date().getTime();
//Указываем параметры запроса «text», для фильтрации истории в диапазоне последнего часа
var query = {
    "text" : "apress",
    "startTime" : currentTimeAsMilliseconds - 6 * tenMinutesAsMilliseconds,
    "endTime" : currentTimeAsMilliseconds,
    "maxResults" : 10
};
//end-region

//region {вычисления}
console.log(greeting);
chrome.history.search(query,function(results) {
    results.forEach(function(result) {
        //Получаем результат типа HistoryItem
        console.log(result);
    });
});
chrome.history.getVisits({"url" : "http://www.example.org"},function(results) {
    results.forEach(function(result) {
        //Получаем результат типа VisitItem
        console.log(result);
    });
});
chrome.history.addUrl({"url" : "http://www.example.org"},function() {
    console.log("addUrl");
});
chrome.history.deleteUrl({"url" : "http://www.example.org"},function() {
    console.log("deleteUrl");
});
/*
chrome.history.deleteAll(function() {
    console.log("deleteAll");
});
*/
//end-region
```

Для поиска в истории браузера используется метод `chrome.history.search`. Он принимает два параметра `query` \(тип объект\) и параметр `callback` \(тип функция\). Параметр query имеет следующие свойства:

* `text` – любой текст для поиска в истории посещённых страниц. Если данное свойство пустое, то будет возвращена вся история.
* `startTime` – содержит дату в миллисекундах с которой выполняется выборка данных из истории.
* `endTime` - содержит дату в миллисекундах до которой выполняется выборка данных из истории.
* `maxResults` - количество записей для извлечения. По умолчанию 100. 

Callback-функция принимает результат виде массива с элементами типа `HistoryItem`. Сам объект `HistoryItem` содержит свойства: `id`, `url`, `title`, `lastVisitTime`, `visitCount` и множество других.

Для получения истории посещения по определённому URL используйте метод `chrome.history.getVisits`. Он принимает первым параметром объект с URL-ом, а вторым callback-функцию, которая принимает результат виде массив с `VisitItem`. Пример использования показан в листинге 3-26.

> **Примечание:**  
> `VisitItem` - это объект, содержащий один визит. Она состоит следующие свойств: `id`, `visitId`, `visitTime`, `referringVisitId` и `transition`. Узнать больше вы можете по ссылке [https://developer.chrome.com/extensions/history](https://developer.chrome.com/extensions/history).



