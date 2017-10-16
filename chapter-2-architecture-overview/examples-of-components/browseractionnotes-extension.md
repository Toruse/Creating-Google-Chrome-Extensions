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





