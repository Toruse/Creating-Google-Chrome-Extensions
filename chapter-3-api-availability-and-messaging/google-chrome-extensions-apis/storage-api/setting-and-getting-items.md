#### Установка и получение элементов

Вы можете установить и получить данные из хранилища используя следующие методы `chrome.storage.sync.set`, и `chrome.storage.sync.get`. Метод `get` принимает в качестве первого параметра строку, или массив строк, или объект, а метод `set` принимает первым параметром только объект \(пара ключ-значение\). Второй параметр `get` метода является callback-функция, которая принимает объект. На рисунке 3-35 в панели разработчика показаны логи вызовов этих методов.



