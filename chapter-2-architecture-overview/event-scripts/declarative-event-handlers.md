### Декларирование обработчика событий

Перед изучением декларирования событий, рассмотрим расширение HelloPageAction.

##### Листинг 2-6. _Chapter2/HelloPageAction/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "HelloPageAction",
    "description" : "Демонстрационное расширение Page-Action",
    "version" : "1.2",
    "page_action" : {
        "default_title" : "HelloPageAction",
        "default_icon" : "icon.png",
        "default_popup" : "popup.html"
    },
        "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : false
    },
    "permissions" : [
        "tabs"
    ]
}
```



