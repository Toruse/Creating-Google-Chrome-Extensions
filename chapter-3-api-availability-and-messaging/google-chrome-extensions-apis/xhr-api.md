### XHR API

Используя объект `XMLHttpRequest` расширение может общаться с удаленными серверами путем отправки и получения запросов. Для таких расширений нужно указать доступ к одному или нескольким хостам в файле манифесте \(обратите внимание на строку `“*://localhost/*”` в листинге 3-31\).

##### Листинг 3-31. _Chapter3/XHRAPI/event\_script.js_

```
{
    "manifest_version" : 2,
    "name" : "API Demos: xhr API",
    "description" : "Demonstrates use of the xhr API",
    "version" : "1.2",
    "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : false
    },
    "permissions" : [
        "*://localhost/*"
    ]
}
```

Когда доступы к хосту указана, то появляется возможность использовать XHR API, как и на обычных веб-страницах. В листинге 3-32 обратите внимание на переменную `ucService` в которой находиться ссылка на локальный сервер HTTP. PHP скрипт указан в листинге 3-33.

##### Листинг 3-32. _Chapter3/TabsAPI/event\_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var xhr = new XMLHttpRequest();
function onReadyStateChange() {
    if(xhr.readyState == 4) {
        console.log(xhr.responseText);
    }
}
var host = "http://localhost/";
var ucService = host + "webpage.php?";
var queryString = "name=" + encodeURIComponent("xhr api");
//end-region

//region {вычисления}
console.log(greeting);
xhr.onreadystatechange = onReadyStateChange;
xhr.open("GET",ucService + queryString);
xhr.send();
//end-region
```

Строка запроса `“name=xhr api”` создаётся статическим способом. Так же она может быть сгенерирована динамически, например, из всплывающего окна Browser-Action или Content-UI.

На рисунке 3-37 показан ответ на запрос от сервера.







