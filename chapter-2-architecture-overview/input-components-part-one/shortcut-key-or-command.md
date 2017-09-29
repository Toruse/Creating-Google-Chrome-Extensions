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



