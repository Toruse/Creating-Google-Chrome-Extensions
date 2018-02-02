### Tabs API

Tabs API \(`chrome.tabs`\) используется для создания, изменения, взаимодействия и сортировки вкладок браузера. Пример использования данного API показан в листинге 3-29. Как видно, в указанном коде используются ранее рассмотренные методы `query`, `connect`, `sendMessage`, `executeScript`, и `insertCSS`, а в этом разделе познакомимся с ещё новыми методами.

> **Примечание:**  
> Вы можете использовать большинство методов и событий `chrome.tabs` , не объявляя никаких доступов. Однако, если вам потребуются свойства `URL`, `title` или `favIconUrl` объекта `tabs.Tab`, то нужно будет указать доступ `tabs` в файле манифесте.

##### Листинг 3-29. _Chapter3/TabsAPI/event_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var createProperties = {
    url : "http://www.example.org",
    active : false,
};
var updateProperties = {
    pinned : true
};
function getJavaScriptCode(dataUrl) {
    var javascriptCode = "var imgElement = document.createElement('img');";
    javascriptCode += "document.body.appendChild(imgElement);";
    javascriptCode += "imgElement.style.borderTop = '2px dashed silver';";
    javascriptCode += "imgElement.src = ";
    javascriptCode += "'" + dataUrl + "';";
    return javascriptCode;
}
function createAndUpdateTab(tab) {
    chrome.tabs.create(createProperties,function(tab) {
        console.log("create");
        //целое или массив целых чисел
        //chrome.tabs.remove(tab.id);
        /*
        chrome.tabs.duplicate(tab.id,function(tab) {
            console.log("duplicate");
        });
        */
        chrome.tabs.update(tab.id,updateProperties,function(tab) {
            console.log("update");
            //chrome.tabs.reload(tab.id);
            chrome.tabs.getZoom(tab.id,function(zoomFactor) {
                console.log("getZoom");
                console.log(zoomFactor); //1
            });
            /*
            chrome.tabs.setZoom(tab.id,2,function() {
                console.log("setZoom");
            });
            */
        });
    });
}
//end-region

//region {вычисления}
console.log(greeting);
chrome.browserAction.onClicked.addListener(function(tab) {
    chrome.tabs.captureVisibleTab({"format":"png"},function(dataUrl) {
        //Не удается получить доступ к chrome:// URL
        chrome.tabs.executeScript(tab.id,{"code":getJavaScriptCode(dataUrl)});
    });
    //createAndUpdateTab(tab);
});
//end-region
```









