#### Сравнение Sync и Local хранение

Для хранения пользовательских данных в расширении, можно использовать `storage.sync` или `storage.local`. При использовании `storage.sync`, сохраненные данные будут автоматически синхронизироваться с любым браузером Chrome, если пользователь вошел в систему и включил синхронизацию. Когда не соединение с сетью, то данные сохраняются локально. При дальнейшем присоединении к сети данные будут автоматически синхронизированы. 

Если у пользователя отключена синхронизация, `storage.sync` будет работать, и вести себя как `storage.local`.

> **Примечание:**
> Конфиденциальную информацию пользователя не следует сохранять данным способом так как они не шифруется!

##### Листинг 3-28. _Chapter3/StorageAPI/event_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
//end-region

//region {вычисления}
console.log(greeting);
/*
//один ключ или список ключей для удаления
chrome.storage.sync.remove("color",function() {
    console.log("remove");
    chrome.storage.sync.get("color",function(items) {
        console.log("get");
        console.log(items);
    });
});
*/
chrome.storage.sync.set({"color":"red"},function() {
    console.log("set");
    //строка или массив строк или объект
    chrome.storage.sync.get("color",function(items) {
        console.log("get");
        console.log(items);
    });
});
chrome.storage.onChanged.addListener(function(changes,areaName) {
    console.log(changes);
    //"sync","local" или "managed"
    console.log(areaName);
});
```





