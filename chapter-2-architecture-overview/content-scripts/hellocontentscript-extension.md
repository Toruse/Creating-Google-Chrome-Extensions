### Расширение HelloContentScript

Данное расширение подключает контент скрипты с помощью параметра манифеста `content_scripts`, а также программно через событие.

Рассмотрим первый способ. В листинге 2-11 для добавления скриптов задан параметр `matches`. Где указан шаблон начиняющийся с символа звездочка \(\*\). Она означает, что адрес может начинаться с HTTP, HTTPS, или иметь другого значения. Аналогичная, звездочка находится в конце шаблона, что означает за именем хоста stackoverflow.com может следовать любой путь. Результат добавления контент сценария \(content\_script.js\) показано на рисунке 2-16.

![Рисунок 2-16. Добавление контент сценария](/assets/figure-2-16.png)

##### Рисунок 2-16. _Добавление контент сценария._

##### Листинг 2-12. _Chapter2/HelloContentScript/event_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World! - from event_script.js";
var cssCode = "a {text-decoration:underline !important;}";
cssCode += "div {background-color:#999 !important;}";
var javascriptCode = "var imgElement = document.createElement('img');";
javascriptCode += "imgElement.src = 'http://placehold.it/350x150';";
javascriptCode += "document.body.appendChild(imgElement);";
//end-region

//region {выполнение}
console.log(consoleGreeting);
chrome.browserAction.onClicked.addListener(function(tab) {
    chrome.tabs.insertCSS(
        {
            //Для подключения CSS файла нужно указать
            //file : "mystyles.css",
            code : cssCode
        },
        function() {
            console.log("CSS inserted!");
        }
    );
    chrome.tabs.executeScript(
        {
            //Для подключения JavaScript файла нужно указать
            //file : "content_script.js",
            code : javascriptCode
        },
        function() {
            console.log("JavaScript executed!");
        }
    );
});
//end-region
```

