### Alarms API

Alarms API \(`chrome.alarms`\) используется для периодического запуска кода или в определённое время. Для него нужно указать в файле манифесте доступ `alarms`. В листинге 3-23 указан код расширения с использованием Alarms.

![Рисунок 3-30. Демонстрация API: Notifications API](/assets/figure-3-30.png)

##### Рисунок 3-30. _Демонстрация API: Notifications API._

Для создания alarm используется метод `chrome.alarms.create`, который принимает два параметра `alarmName`\(тип строка\) и `alarmInfo`\(объект\). В `alarmInfo`входит описание, когда и как должна выполниться задача. Начало выполнения указывается в свойстве `when`или `delayInMinutes`.

![Рисунок 3-31. Демонстрация API: Notifications API](/assets/figure-3-31.png)

##### Рисунок 3-31. _Демонстрация API: Notifications API._

Если задан параметр `periodInMinutes`, то Alarm спустя указанных минут, будет периодично выполнять слушатель `chrome.alarms.onAlarm`. Сам слушатель получает функцию callback, в которую передаётся объект Alarm, содержащий имя, запланированное время \(`scheduledTime`\) и `periodInMinutes`. Результат работы данного расширения показан на рисунке 3-26.

![Рисунок 3-32. Демонстрация API: Notifications API](/assets/figure-3-32.png)

##### Рисунок 3-32. _Демонстрация API: Notifications API._

> **Примечание:**
> Предела в количестве вызовов alarm нет, но для уменьшения нагрузки, минимальный интервал между двумя вызовами составляет одну минуту.

##### Листинг 3-23. _Chapter3/AlarmsAPI/event_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var count = 0;
var alarmName = "testAlarm";
var alarmInfo = {
    when : Date.now() + 6000,
    periodInMinutes : 1 //Вызываем каждую минуту
};
//end-region

//region {вычисления}
console.log(greeting);
chrome.alarms.clearAll();
chrome.alarms.onAlarm.addListener(function(alarm) {
    console.log("onAlarm-" + ++count);
});
chrome.alarms.create(alarmName,alarmInfo);
//end-region
```





