### Content сценарии

При написании content-сценария в целях безопасности вы обязаны выполнять проверку вводимых данных от пользователя. Так же нужно проверять на корректность данные получаемые от удалённых сервисов.  

> **Примечание:**
> Content-сценарии выполняться в изолированной среде. Они имеют доступ к DOM веб-страницы, но не имеют общих переменных и функций с веб-страницей. Также и выполняемы JavaScript не имеет доступа к переменным и функциям content-сценария.
>
> Что касается общих объектов для этих сценариев, например window.onload, то каждая среда имеет свою версию данного объекта.

Хотя изолированная среда обеспечиваем защиту от вредоносных веб-страниц и удаленных сервисов, но это не гарантирует полную защиту от атак на content-сценарий. Например, использование метода `eval`, позволяет выполнить вредоносный код. Чтобы избежать этот ситуации нужно использовать более безопасный метод `JSON.parse`.




