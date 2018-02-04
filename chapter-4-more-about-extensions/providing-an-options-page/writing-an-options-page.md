### Сохранение настроек

Страница настроек строиться на основе HTML-страницы \(Рисунок 4-4\). В листинге 4-2 показан пример реализации данной страницы для расширения OverridePages.

> **Примечание:**  
> Чтобы программно открыть страницу настроек, используйте метод `chrome.runtime.openOptionsPage`.

![Рисунок 4-1. Новая вкладка: сообщение переопределения](/assets/figure-4-1.png)

##### Рисунок 4-1. _Новая вкладка: сообщение переопределения._

##### Листинг 4-2. _Chapter4/OverridePages/myOptionsPage.html_

```
<!DOCTYPE html>
<html>
    <head>
        <title>Моя страница с настройками</title>
        <script src="myOptionsPage_1.js"></script>
        <style>
            div.left {
                float:left;
            }
            div.right {
                float:right;
            }
            p.clear {
                clear:both;
            }
        </style>
    </head>
    <body>
        <p>
            <div class="left">
                Закладки, соответствующие правилу?
            </div>
            <div class="right">
                <form>
                    <input type="radio" name="highlight" value="1"> Да
                    <input type="radio" name="highlight" value="0" checked="checked"> Нет
                </form>
            </div>
        </p>
        <br>
        <p class="clear">
            <input type="button" id="save" value="Сохранить">
        </p>
    </body>
</html>
```

К странице настроек можно подключать сценарии, указав в атрибуте `src` путь относительно папки расширения. В листинге 4-2 показано как подключается сценарий myOptionsPage\_1.js, а в листинге 4-3 содержится код самого сценария. Указанный скрипт выполняет сохранение пользовательских настроек для расширения OverridePages.

##### Листинг 4-3. _Chapter4/OverridePages/myOptionsPage_1.js_

```
//region {переменные и функции}
var storageKey = "APPEND_MATCHING_ONLY";
var items = {};
var saveButtonID = "save";
function logSuccess(task) {
    console.log("%s Successful!",task);
}
//end-region

//region {вычисления}
document.addEventListener("DOMContentLoaded",function(dcle) {
    var saveButton = document.getElementById(saveButtonID);
    saveButton.addEventListener("click",function(ce) {
        if(document.forms[0].highlight.value == "1") {
            items[storageKey] = true;
            chrome.storage.sync.set(
                items,
                function(){if(!chrome.runtime.lastError)logSuccess("Set-Storage");}
            );
        } else {
            items[storageKey] = false;
            chrome.storage.sync.set(
                items,
                function(){if(!chrome.runtime.lastError)logSuccess("Set-Storage");}
            );
        }
    });
});
//end-region
```





