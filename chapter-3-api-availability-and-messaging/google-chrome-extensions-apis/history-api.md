### History API

History API \(`chrome.history`\) используется для работы со списком посещенных страниц. Так же, есть возможность добавлять, удалять и запрашивать URL-адреса из истории браузера. Листинг 3-26 содержит пример использования HistoryAPI.

##### Листинг 3-26. _Chapter3/HistoryAPI/event_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var tenMinutesAsMilliseconds = 10 * 60 * 1000;
//getTime возвращает количеству миллисекунд, прошедших с полуночи 1 января 1970 года GMT
var currentTimeAsMilliseconds = new Date().getTime();
//Указываем параметры запроса «text» для фильтрации истории в диапазоне последнего часа
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

