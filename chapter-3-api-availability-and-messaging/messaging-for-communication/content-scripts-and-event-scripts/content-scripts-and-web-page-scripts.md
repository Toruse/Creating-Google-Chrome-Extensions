#### Content сценарии и Сценарии веб-страницы

Как писалось раньше, content сценарий не имеют доступа к событиям`runtime.onMessageExternal`and `runtime.onConnectExternal`. В замен для отправки сообщений можно использовать стандартный API JavaScript. Чтобы понять как это работает, рассмотрим расширений CSandWS. Код показан в листинге 3-17 и 3-19.

На основе атрибута `content_scripts` файла манифеста, происходит добавление сценария на веб-страницу, которая находиться на локальном сервере. Однако данный пример возможно реализовать и без локального хоста, указав в атрибуте \*.

##### Листинг 3-17. _Chapter3/CSandWS/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "Communication Demo: content-script and webpage-script",
    "description" : "Показывает связь content-сценария и webpage-сценария",
    "version" : "1.2",
    "content_scripts" : [
        {
            "matches" : ["*://localhost/*"],
            "js" : ["content_script.js"]
        }
    ]
}
```

> **Примечание:**  
> Веб-страница предоставленная для расширения запускается на локальном сервере. Несмотря на то, что основной файл веб-страницы - это PHP файл, он содержит простой HTML-код. Соответственно его можно открыть и просмотреть в браузере Chrome.

Листинг 3-18 содержит код content-сценария, который создает кнопку «Send Message» на веб-странице \(Рисунок 3-22\). Так же данной кнопке назначается слушатель нажатия - `click`. Он в свою очередь отправляет в консоль сообщение «Button clicked!», и вызывает метод `window.postMessage(message,targetOrigin)`.

В указанном выше методе первый аргумент `message`содержит само сообщение, а второй `targetOrigin`содержит URI окна получателя. В данном варианте указывается адрес текущего окна: `var targetOrigin = window.location.origin`. Однако не допускаются значения: `"file://"`,`"file://*"`, `""`, и `null`. Чтобы использовать API обмена сообщениями на локальной веб-странице, `postMessage`нужно вызвать с такими параметрами `window.postMessage (сообщение, "*")`.

> **Примечание:**  
> Для того, чтобы подключить content-сценарий к локальной веб-странице, нужно в атрибуте `"matches"` указать значение: `["file://*"]`.

Независимо от указанного получателя сообщений \(http://, https:// или file://\), функция перехватчик должны иметь вид `window.addEventListener("message", function(me){/**/})` \(Листинг 3-19\). Сама функция слушатель сообщений принимает объект отправленный методом `postMessage`, при помощи, которого можно получить доступ к передаваемой строке или объекту. Результат работы расширения показан на рисунке 3-22.

![Рисунок 3-27. Демонстрация API: Bookmarks API](/assets/figure-3-27.png)

##### Рисунок 3-27. _Демонстрация API: Bookmarks API._

##### Листинг 3-18. _Chapter3/CSandWS/content_script.js_

```
//region {переменные и функции}
var consoleGreeting = "Hello World!";
var targetOrigin = window.location.origin;
var message = "Test message X";
function createButton() {
    var button = document.createElement("button");
    button.style.width = "70px";
    button.style.height = "40px";
    button.style.position = "fixed";
    button.style.top = "10px";
    button.style.right = "10px";
    button.innerText = "Send Message";
    document.body.appendChild(button);
    return button;
}
//end-region

//region {вычисления}
console.log(consoleGreeting);
var button = createButton();
button.addEventListener("click",function() {
    console.log("Button clicked!");
    window.postMessage(message,targetOrigin);
});
/*
window.addEventListener("message",function(me) {
    console.log("message: " + me.data);
});
*/
//end-region
```



