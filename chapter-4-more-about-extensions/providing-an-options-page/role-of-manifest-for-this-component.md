### Роль манифеста

Для того, чтобы зарегистрировать страницу настроек нужно использовать атрибут `options_ui` в файле манифесте. Как видно из листинга 4-1 \(расширение OverridePages\), достаточно указать свойство `chrome_style`, чтобы объявить страницу настроек для расширения. Так же данный атрибут поддерживает следующие свойства:

* `page` \(строка\) - путь к странице настроек, относительно корня расширения.
* `chrome_style` \(логическое значение\) - если истина, то Google Chrome будет применять пользовательские стили к странице настроек. Значение по умолчанию `false`, но рекомендуется указывать `true`, для согласования пользовательского интерфейса с Chrome,
* open\_in\_tab \(логическое значение\) - если истина, страница настроек будет открыта в новой вкладке, а не в менеджере расширений \(chrome://extensions/\). По умолчанию установлено значение `false`.

##### Листинг 4-1. _Chapter4/OverridePages/manifest.json_

```
{
    "name" : "My New-Tab",
    "version" : "1.2",
    "manifest_version" : 2,
    "chrome_url_overrides" : {
        /*newtab,history,bookmarks*/
        "newtab" : "myNewTab.html"
    },
    "permissions" : ["bookmarks","storage"],
    /*Using an options page*/
    "options_ui" : {
        "page" : "myOptionsPage.html",
        /*Use Chrome stylesheet*/
        "chrome_style" : true
    }
}
```



