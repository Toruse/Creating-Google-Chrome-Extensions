### Клавиши быстрого доступа

Для быстрого вызова расширения и ввода данных назначаются горячие клавиши. По умолчанию комбинации клавиш указывается в манифесте в параметре commands, как показано в листинге 2-4. Максимальное количество комбинаций для различных действий в данной параметре может быть указано четыре.

##### Листинг 2-4. _Chapter2/HelloShortcutKey/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "HelloShortcutKey",
    "description" : "Демонстрация использования горячих клавиш",
    "version" : "1.2",
    "browser_action" : {
        "default_title" : "HelloShortcutKey",
        "default_icon" : "icon-1.png"
    },
    "background" : {
        "scripts" : ["event_script.js","another_event_script.js"],
        "persistent" : false
    },
    "commands" : {
        "shortcut-key to change the extension icon" : {
            "suggested_key" : {"default" : "Alt+Shift+9"},
            "description" : "Изменить иконку расширения"
        }
    }
}
```

В листинге 2-4, указывается только одна комбинация клавиш быстрого доступа. В атрибуте commands прописан объект с идентификатором «shortcut-key to change the extension icon», который имеет свойства suggested\_key, где указывается через параметр default комбинацию клавиш.

Так же пользователь может самостоятельно указать данные комбинации клавиш по адресу chrome://extensions/configureCommands \(см рисунок 2-6 и 2-7\). Для работы с комбинациями из сценария используется объект chrome.commands.

![Рисунок 2-6. Регистрация комбинации клавиш для расширения HelloBrowserAction](/assets/figure-2-5.png)

##### Рисунок 2-6. _Регистрация комбинации клавиш для расширения HelloBrowserAction._




