### Расширение BrowserActionNotes

Данное расширение позволяет делать заметки к веб-странице. Для этих целей используется компонент Browser-Action \(см. рисунок 2-20\) и Popup компонент \(рисунок 2-21\). Расширение может добавить только одну заметку для одного URL. Заметка может быть перезаписана и удалена.

![Рисунок 2-20. BrowserActionNotes: компонент Browser-Action](/assets/figure-2-20.png)

##### Рисунок 2-20. _BrowserActionNotes: компонент Browser-Action._

![Рисунок 2-21. BrowserActionNotes: Popup компонент](/assets/figure-2-21.png)

##### Рисунок 2-21. _BrowserActionNotes: Popup компонент._

Popup окно содержит элемент textarea и две кнопки SAVE и REMOVE. Textarea используется для указания сохраняемой заметки \(как показано на рисунке 2-22\). HTML Popup окна указан в листинг 2-13. Обратите внимание, как происходит в коде взаимодействие с элементом textarea, и тегами кнопок.

![Рисунок 2-22. BrowserActionNotes: Popup компонент](/assets/figure-2-22.png)

##### Рисунок 2-22. _BrowserActionNotes: Popup компонент._

Также к всплывающему окну расширения подключается скрипт popup\_script.js. Для сохранения заметки используется элемент API `localStorage`. После нажатия кнопки SAVE заметка записывается в локальное хранилище под ключом, который соответствует URL-адресу \(рисунок 2-23\), а кнопка REMOVE соответственно удаляет заметку.

![Рисунок 2-23. BrowserActionNotes: Панель Application](/assets/figure-2-23.png)

##### Рисунок 2-23. _BrowserActionNotes: Панель Application._

##### Листинг 2-13. _Chapter2/BrowserActionNotes/popup.html_

```
<script src="popup_script.js"></script>

<style>
...
</style>
</head>
<body>
     <div id="container">
          <div id="top"><textarea id="note" placeholder="..."></textarea></div>
          <div id="bottom">
               <br>
               <button id="save_button">SAVE</button>
               <br>
               <button id="remove_button">REMOVE</button>
          </div>
     </div>
</body>
</html>
```

После загрузки Popup сценария, при помощи метода `getElementById`устанавливается связь с элементами textarea и кнопками. В листинге 2-14 так же указаны основные функции `hardSave`и `removeNote`для работы с заметками, которые используют API вкладок браузера. Не забудьте указать разрешение на использование вкладок в файле манифесте.

После нажатия кнопки SAVE отработает функция `hardSave`, которая при помощи метода `localStorage.setItem(activeURL,noteText)` сохранит заметку. При нажатии кнопки REMOVE отработает функция `removeNote`, и удалит заметку используя метод `localStorage.removeItem`.

##### Листинг 2-14. _Chapter2/BrowserActionNotes/popup\_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World! - from popup_script.js";
//Также можно прокешировать активный URL вкладки
//var activeURL = "";
var noteElementID = "note";
var saveButtonID = "save_button";
var removeButtonID = "remove_button";
var noteElement = null;
var saveButton = null;
var removeButton = null;
var queryInfo = {"active":true};
function logSuccess(task) {
    console.log("%s Successful!",task);
    chrome.browserAction.setBadgeText({"text":localStorage.length.toString()});
}
//function logFailure(task) {console.log("%s Failed!",task);}
function loadNoteForActiveURL(noteElement) {
    chrome.tabs.query(queryInfo,function(tabs) {
        var activeURL = tabs[0].url;
        noteElement.value = localStorage.getItem(activeURL);
        logSuccess("Get-Storage");
    });
}
function softSave(noteText) {}
function hardSave(noteText) { //Прописываем значение
    chrome.tabs.query(queryInfo,function(tabs) {
        var activeURL = tabs[0].url;
        localStorage.setItem(activeURL,noteText);
        logSuccess("Set-Storage");
    });
}
function removeNote() {
    chrome.tabs.query(queryInfo,function(tabs) {
        var activeURL = tabs[0].url;
        localStorage.removeItem(activeURL);
        logSuccess("Remove-Storage");
    });
}
//end-region
```

При открытии всплывающего окна расширения, выполняется функция `loadNoteForActiveURL`\(Листинг 2-15\). Она получает данные из `localStorage`на основе адреса активной вкладки, и передаёт элементу textarea. Для вывода результатов работы расширения используется функция логирования `logSuccess`. Чтобы показать количество заметок на кнопке Browser-Action используется `localStorage.length`. Результат работы расширения показан на рисунке 2-24 и 2-25.

![Рисунок 2-24. BrowserActionNotes: Установка значения на иконке](/assets/figure-2-24.png)

##### Рисунок 2-24. _BrowserActionNotes: Установка значения на иконке._

![Рисунок 2-25. BrowserActionNotes: Консольная панель](/assets/figure-2-25.png)

##### Рисунок 2-25. _BrowserActionNotes: Консольная панель._

> **Примечание:**  
> Пометка, которая находиться на Browser-Action, позволяет отобразить краткую информацию о состоянии расширения. Длинная данного сообщения не должна превышать 4 символа.   
> Вы легко можете задать текст и цвет пометки при помощи методов `browserAction.setBadgeText` и `browserAction.setBadgeBackgroundColor`.

##### Листинг 2-15. _Chapter2/BrowserActionNotes/popup\_script.js_

```
//region {вычисление}
console.log(consoleGreeting);
document.addEventListener('DOMContentLoaded',function(dcle) {
    saveButton = document.getElementById(saveButtonID);
    removeButton = document.getElementById(removeButtonID);
    noteElement = document.getElementById(noteElementID);

    //Загрузка заметки для активного URL (если она была сохранена)
    loadNoteForActiveURL(noteElement);
    chrome.browserAction.setBadgeBackgroundColor({"color":[255,0,0,255]})
    //Добавляем слушатель на нажатие кнопки
    saveButton.addEventListener('click',function(ce) {
        var noteText = noteElement.value;
        if(noteText.length > 0) hardSave(noteText);
    });
    removeButton.addEventListener('click',function(ce) {
        removeNote();
    });
});
//end-region
```



