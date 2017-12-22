### Popup и Event сценарии

Теперь давайте посмотрим, как сценарий popup-окна взаимодействует с event-сценарием. 

В расширении они выполняются в одной среде, но это два разными компонента. Соответственно должен присутствовать механизм общения между ними, и он на много проще предыдущих. 

##### Листинг 3-20. _Chapter3/PSandES/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "Communication Demo: popup-script and event-script",
    "description" : "Показывает связь popup-сценария и event-сценария",
    "version" : "1.2",
    "browser_action" : {
        "default_title" : "Communication Demo: popup-script and event-script",
        "default_icon" : "icon.png",
        "default_popup" : "popup.html"
    },
    "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : false
    }
}
```


