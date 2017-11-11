### Элементы контекстного меню

Chrome Extensions позволяет использовать контекстное меню. Создавать в нем новые пункты, как показано на рисунке 3-10. Так же можно создавать под меню, что позволит сгруппировать функционал расширения. Чтобы начать работать с данным компонентом, нужно указать в файле манифеста разрешение contextMenus.

##### Листинг 3-3. _Chapter3/HelloContextMenuItem/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "HelloContextMenuItem",
    "description" : "Расширение для демонстрации контекстного меню",
    "version" : "1.2",
    "permissions" : ["contextMenus"],
    "icons" : {
        "16" : "icon-16.png",
        "128" : "icon-128.png"
    },
    "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : true
    }
}
```



