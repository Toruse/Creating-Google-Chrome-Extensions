#### Обновление вкладки

Чтобы изменить свойства вкладки используется метод `chrome.tabs.update`. Этот метод принимает три параметра `tabId`, `updateProperties`, и `callback`. `TabId` - это идентификатор вкладки, объект `updateProperties` содержит обновляемые свойства, а callback-функция через объект `Tab` получает информацию об изменяемой вкладке. Для редактирования доступны следующие свойства: `url`, `active`, `highlighted`, `pinned`, `muted`, и `openerTabId`. Вы также можете перезагрузить вкладку вызвав метод `chrome.tabs.reload`, который принимает в качестве первого параметра идентификатор вкладки и необязательный второй параметр callback-функцию.

##### Листинг 3-30. _ Chapter3/TabsAPI/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "API Demos: tabs API",
    "description" : "Demonstrates use of the tabs API",
    "version" : "1.2",
    "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : false
    },
    "browser_action" : {
        "default_icon" : "icon.png"
    },
    "permissions" : [
        "tabs",
        "<all_urls>"
    ]
}
```












