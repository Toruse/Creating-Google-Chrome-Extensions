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





