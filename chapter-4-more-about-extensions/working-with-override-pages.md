## Работа с переопределённой страницей

Переопределённые страницы – это способ заменить стандартные страницы Google Chrome на страницы вашего расширения. Для переопределения доступны следующие страницы:

* Менеджер закладок \(`chrome://bookmarks`\) - это страница показывается, когда пользователь выбирает пункт меню "Chrome\Закладки\Диспетчер закладок".
* История \(`chrome://history`\) – страница показывается, когда пользователь выбирает пункт меню "Chrome\История\История".
* Новая вкладка \(`chrome://newtab`\) – страница показывается, когда пользователь создает новую вкладку или окно.

![Рисунок 4-2. Новая вкладка с закладками](/assets/figure-4-2.png)

##### Рисунок 4-2. _Новая вкладка с закладками._

> **Примечание:**
> Расширение может переопределить только одну страницу. Так, например, расширение OverridePages переопределяет страницу Новая вкладка \(New Tab\).

##### Листинг 4-4. _Chapter4/OverridePages/myNewTab.html_

```
<!DOCTYPE html>
<html>
    <head>
        <title>Моя новая вкладка</title>
        <script src="myNewTab_1.js"></script>
        <style>
            body {
                background-color:#eee;
            }
            h2 {
                width:50%;
                margin:auto auto;
                text-align:center;
                color:#555;
            }
            ul {
                padding:0px;
                width:60%;
                margin-left:auto;
                margin-right:auto;
                margin-top:100px;
                text-align:center;
                border:2px dashed #555;
            }
            li {
                overflow:hidden;
                list-style-type:none;
            }
            a {
                text-decoration:none;
            }
            a:hover {
                text-decoration:underline;
            }
        </style>
    </head>
    <body>
        <h2>Моя новая вкладка: Chrome Разработка Закладки</h2>
        <ul id="list"></ul>
    </body>
</html>
```


