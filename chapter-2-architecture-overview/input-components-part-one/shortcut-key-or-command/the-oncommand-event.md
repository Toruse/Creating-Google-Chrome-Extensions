#### Событие onCommand

После определения клавиш быстрого доступа для расширения, вы можете указать свою функцию слушатель при помощи метода `onCommand`\(`chrome.commands.onCommand`\).

##### Листинг 2-5. _Chapter2/HelloShortcutKey/event\_script.js_

```
//region {variables and functions}
var consoleGreeting = "Hello World! - from event_script.js";
var details = {"path":"icon-2.png"};
//end-region

//region {calls}
console.log(consoleGreeting);
chrome.commands.onCommand.addListener(function(command) {
    chrome.browserAction.setIcon(
        details,
        function() {/**/}
    );
});
//end-region
```

В листинге 2-4 и 2-5 наведён пример кода из расширения HelloShortcutKey. Данное расширение для Browser-Action устанавливает иконку, загруженную из файла icon-1.png. С помощью слушателя onCommand и метода  chrome.browserAction.setIcon происходит замена иконки на icon-2.png \(Рисунок 2-9\).

![Рисунок 2-9. Файлы расширения HelloShortcutKey](/assets/figure-2-9.png)

##### Рисунок 2-9. _Файлы расширения HelloShortcutKey._

Как видно из листинга 2-5, метод addListener используется для подключения к onCommand функцию обработчик события. Соответственно функция получает строковый аргумент «command», который содержит имя идентификатора \(например: “shortcut-key to change the extension icon”\) нажатых горячих клавиш. Сама функция меняет иконки расширения.

Указанный аргумент полезен, когда в манифесте задано больше одной комбинации клавиш. Для того, чтобы определить какую команду нужно выполнить желательно расширить функцию с помощью оператора `switch`.

> **Примечание:**  
> Не запутайтесь между методами addListener и addEventListener. Последний относится к DOM API.



