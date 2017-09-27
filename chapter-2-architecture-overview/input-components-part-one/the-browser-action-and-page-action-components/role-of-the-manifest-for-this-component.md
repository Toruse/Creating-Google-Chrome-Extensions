#### Роль манифеста

Чтобы получить возможность использовать Browser-Action и Page-Action, их нужно объявить в файле манифесте. Пример для Browser-Action указан в листинге 2-2.

##### Листинг 2-2. _Chapter2/HelloBrowserAction/manifest.json_

```
"browser_action" : {
    "default_title" : "HelloBrowserAction",
    "default_icon" : "icon.png",
    "default_popup" : "popup.html"
}
```

Аналогичным образом, в листинг 2-3 показано, как объявить Page-Action. Напоминаем, что расширение может использовать только один из компонентов Browser-Action или Page-Action.

##### Листинг 2-3. _Chapter2/HelloPageAction/manifest.json_

```
"page_action" : {
    "default_title" : "HelloPageAction",
    "default_icon" : "icon.png",
    "default_popup" : "popup.html"
}
```

При добавлении browser\_action или page\_action нужно указать соответствующие параметры:

* default\_title - всплывающая подсказка для расширения
* default\_icon – путь к png-изображению
* default\_popup – путь к HTML-файлу, который содержит разметку для всплывающего окна расширения

> **Примечание:**  
> Все пути ресурсов, представленные в файле манифеста, указываются относительно корневой папки расширения. Например, если у вас есть папка с именем `HelloWorldExtension`которая содержит манифест, то по умолчанию, иконка «icon.png» будет взята из корневой папки.



