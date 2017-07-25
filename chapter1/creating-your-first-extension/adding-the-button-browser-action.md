### Добавляем кнопку: Browser-Action

Чтобы кнопка расширения отобразилась на панели инструментов браузера Google Chrome, нужно указать в манифесте атрибут _browser\_action_. Он имеет тип - объект \(то есть {}\), который включает в себя следующие свойства: _default\_title_, _default\_icon_, и _default\_popup_.

В листинге 1-1 показано, что каждое из этих свойств принимает строковое значение. Для всплывающей подсказки задается свойство _default\_title_. Свойство _default\_icon_ содержит путь к иконке в формате PNG, предназначенной для кнопки расширения Google Chrome, а в свойстве _default\_popup _указывается путь к HTML-файлу, который будет использоваться в качестве всплывающего окна.

##### Листинг 1-1. _ShowTime/manifest.json._

```
{
    "manifest_version" : 2,
    "name" : "ShowTime",
    "description" : "Расширения для вывода текущего времени и даты",
    "version" : "1.2",
    "browser_action": {
        "default_title" : "ShowTime",
        "default_icon" : "icon.png", //Указывается иконка для кнопки на панели инструментов Chrome
        "default_popup" : "popup.html"

    },
    "icons" : {
        "16" : "icon16.png", //Указывается иконка для страницы управления расширением.
        "48" : "icon48.png", //Указывается иконка для страницы управления расширениями.
        "128" : "icon128.png" //Указывается иконка для процедуры установки и для интернет-магазина Chrome.
    }
}
```

Теперь переходим к написанию JavaScript и HTML кода. Процесс создание всплывающего окна ни чем не отличается от создания любой другой статической веб-страницы. Так же вам предоставлены все возможности JavaScript языка. Это означает, что можно использовать объект Date и дерево DOM.

Используя предоставленные возможности, реализуем расширение, как показано в листинге 1-2 и 1-3.

**Листинг 1-2. **_**ShowTime/popup\_script.js**_

```
    //область {variables and functions}
    var timeId = "time";
    var dateId = "date";
    var days = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"];
    var months = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];
    var consoleGreeting = "Hello World! - from popup_script.js";
    function setTimeAndDate(timeElement,dateElement) {
        var date = new Date();
        var minutes = (date.getMinutes() < 10 ? '0' : '') + date.getMinutes();
        var time = date.getHours() + ":" + minutes;
        var date = days[date.getDay()] + ", " + months[date.getMonth()] + " " + date.getDate() + " " + date.getFullYear();
        timeElement.innerHTML = time;
        dateElement.innerHTML = date;
    }
    //конец области
```

В листинге 1-2 объявляется функция setTimeAndDate, которая принимает два аргумента, первый это элемент для вывода времени, второй для вывода даты. Важно заметить, что если метод getMonth возвращает 0, то это соответствует первому месяцу года, а для метода getDay это соответствует день недели - воскресенье.

**Листинг 1-3. **_**ShowTime/popup\_script.js**_

```
    //region {calls}
    console.log(consoleGreeting);
    document.addEventListener("DOMContentLoaded",function(dcle) {
        var timeElement = document.getElementById(timeId);
        var dateElement = document.getElementById(dateId);
        setTimeAndDate(timeElement,dateElement);
    });
    //end-region
```

Листинг 1-3 содержит продолжение код JavaScript, где на документ вешается событие DOMContentLoaded, которое вызывается после загрузки страницы, и соответственно в нем получаем доступ к элементам DOM, и вызывается setTimeAndDate.

**Листинг 1-4. **_**ShowTime/popup.html**_

```
    <!DOCTYPE html>
    <html>
    <head>

    <!-- Следующий тег не выполниться -->
    <title>ShowTime (Custom)</title>

    <!--
    <script>
    // Следующий скрипт не выдаст предупреждение
    alert('Hello World');
    </script>
    -->

    <!-- Подключаем js-скрипт -->
    <script src="popup_script.js"></script>

    <style>
    body {
        padding:0px;
        margin:0px;
        width:300px;
        height:200px;
    }
    div {
        height:100%;
        width:100%;
        display:table;
        font-family:"Tahoma","Verdana";
        font-size:15px;
        font-weight:bold;
        text-shadow:0px 0px 1px #000000;
        background-color:#555;
        color:#fff;
    }
    h1,h2 {
        display:table-row;
        vertical-align:middle;
        text-align:center;
    }
    h2 {
        background-color:#777;
    }
    .unselectable {
        -webkit-user-select:none;
        cursor:default;
    }
    </style>
    </head>
    <body>
        <div class="unselectable">
            <h1 class="empty"></h1>
            <h1 id="time"></h1>
            <h2 id="date"></h2>
        </div>
    </body>
    </html>
```



