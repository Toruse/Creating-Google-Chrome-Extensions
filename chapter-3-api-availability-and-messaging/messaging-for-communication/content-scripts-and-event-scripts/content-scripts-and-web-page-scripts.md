#### Content сценарии и Сценарии веб-страницы

Как писалось раньше, content сценарий не имеют доступа к событиям` runtime.onMessageExternal `and `runtime.onConnectExternal`. В замен для отправки сообщений можно использовать стандартный API JavaScript. Чтобы понять как это работает, рассмотрим расширений CSandWS. Код показан в листинге 3-17 и 3-19.

На основе атрибута `content_scripts` файла манифеста, происходит добавление сценария на веб-страницу, которая находиться на локальном сервере. Однако данный пример возможно реализовать и без локального хоста, указав в атрибуте \*.

##### Листинг 3-17. _Chapter3/CSandWS/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "Communication Demo: popup-script and content-script",
    "description" : "Показывает связь popup-сценария и content-сценария",
    "version" : "1.2",
    "content_scripts" : [
        {
            "matches" : ["*://www.example.org/*"],
            "js" : ["content_script.js"]
        }
    ],
    "browser_action" : {
        "default_title" : "Communication Demo: popup-script and content-script",
        "default_icon" : "icon.png",
        "default_popup" : "popup.html"
    }
}
```







