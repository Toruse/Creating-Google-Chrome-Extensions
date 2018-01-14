### Downloads API

API загрузки \(`chrome.downloads`\) используется для инициализации, поиска и контроля загрузки данных. Для этого нужно указать доступ `downloads` в файле манифеста. Пример использования показан в листинге 3-25.

##### Листинг 3-25. _Chapter3/DownloadsAPI/event_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var downloadOptions = {
    "url" : "https://github.com/Apress/creating-google-chrome-extensions/archive/master.zip",
    "saveAs" : true
};
//end-region

//region {вычисления}
console.log(greeting);
chrome.downloads.download(downloadOptions,function(downloadId) {
    console.log(downloadId);
    /*
    chrome.downloads.pause(downloadId,function() {
        if(!chrome.runtime.lastError) console.log("pause");
    });
    */
});
chrome.downloads.onCreated.addListener(function(downloadItem) {
    console.log("onCreated:");
    console.log(downloadItem);
});
chrome.downloads.onErased.addListener(function(downloadId) {
    console.log("onErased:");
    console.log(downloadId);
});
chrome.downloads.onChanged.addListener(function(downloadDelta) {
    console.log("onChanged:");
    console.log(downloadDelta);
});
```
