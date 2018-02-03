### XHR API

Используя объект `XMLHttpRequest` расширение может общаться с удаленными серверами путем отправки и получения запросов. Для таких расширений нужно указать доступ к одному или нескольким хостам в файле манифесте \(обратите внимание на строку `“*://localhost/*”` в листинге 3-31\).

##### Листинг 3-31. _Chapter3/XHRAPI/manifest.json_

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





