#### Роль событий для этого компонента

Теперь перейдем к сценарию данного расширения. В нём используются слушатели `onInputStarted`, `onInputChanged`, `onInputEntered`, и `onInputCancelled`, которые относятся к `chrome.omnibox`. Так же данному компоненту не нужно указывать разрешения в файле манифесте. Код сценария указан в листинге 3-2.

![Рисунок 3-3. HelloOmniboxInput: Взаимодействие с omnibox](/assets/figure-3-3.png)

##### Рисунок 3-3. _HelloOmniboxInput: Взаимодействие с omnibox._

##### Листинг 3-2. _Chapter3/HelloOmniboxInput/event\_script.js_

```
//region {переменные и функции}
var ON_INPUT_ENTERED_DISPOSITION = {
    "CURRENT_TAB" : "currentTab",
    "NEW_FOREGROUND_TAB" : "newForegroundTab",
    "NEW_BACKGROUND_TAB" : "newBackgroundTab"
};
var suggestResultOne = {
    "content" : "Some content",
    "description" : "Description"
};
var suggestResults = [suggestResultOne];
var searchService = "https://www.google.com/search?q=chrome+extensions+developers+";
function CreateWindow(url) {
    var windowCreateData = {"url" : ""};
    windowCreateData.url = url;
    chrome.windows.create(windowCreateData);
}
var descriptions = {
    "a" : ["actions","alarms","apps",],
    "b" : ["background-page","bookmarks","browser-action"],
    "c" : ["commands","content-script","context-menu"],
    "d" : ["dashboard","declarativeContent"],
    "e" : ["event-script","examples"],
    "h" : ["history"],
    "i" : ["incognito","inject"],
    "m" : ["management page","manifest","match pattern","messaging"],
    "o" : ["omnibox"],
    "p" : ["page-action","permissions","plugins","popup"],
    "r" : ["resources panel","runtime"],
    "s" : ["sources panel","store","storage"],
    "t" : ["tabs","themes"]
};
function getSuggestResults(key) {
    var results = [];
    if(!descriptions[key] || !key) return suggestResults;
    for(var i=0;i<descriptions[key].length;i++) {
        var suggestResult = {};
        suggestResult["content"] = descriptions[key][i];
        suggestResult["description"] = "Search '" + descriptions[key][i] + "' on developer.chrome.com";
        results[i] = suggestResult;
    }
    return results;
}
//end-region

//region {вызовы}
chrome.omnibox.setDefaultSuggestion({"description":"Search on developer.chrome.com"});
chrome.omnibox.onInputStarted.addListener(function() {
    console.log("<InputStarted>");
});
chrome.omnibox.onInputChanged.addListener(function(text,suggest) {
    console.log("<InputChanged> Text: " + text);
    //suggest(suggestResults);
    suggest(getSuggestResults(text));
});
chrome.omnibox.onInputEntered.addListener(function(text,disposition) {
    console.log("<InputEntered> Text: " + text);
    CreateWindow(searchService + text);
    //default disposition is ON_INPUT_ENTERED_DISPOSITION.CURRENT_TAB
});
//end-region
```

![Рисунок 3-4. HelloOmniboxInput: Похожие результаты](/assets/figure-3-4.png)

##### Рисунок 3-4. _HelloOmniboxInput: Похожие результаты._

В сценарии используется два слушателя это `chrome.omnibox.onInputChanged`и `chrome.omnibox.onInputEntered`. Первый отслеживает, что вводится пользователем в адресатной строке, а второй срабатывает, когда закончен ввод данных. Результат работы показан на рисунке 3-6.

![Рисунок 3-5. HelloOmniboxInput: Взаимодействие с omnibox](/assets/figure-3-5.png)

##### Рисунок 3-5. _HelloOmniboxInput: Взаимодействие с omnibox._

Обработчик событий`onInputChanged`генерирует результат виде массива, каждый элемент которого имеет свойства `content`– содержание и `description`– описание. Пример наведён ниже:

```
var suggestResultOne = {
    "content" : "Some content",
    "description" : "Description"
};
```

При вводе символов в адресатной строке браузера, идет переборка массива ключевых слов, из которого генерируется выпадающий список подсказок, как показано на рисунок 3-4 и 3-5. Если ничего не найдено, то подставляется значение из переменной `suggestResults`. Обратите внимание, что для каждого элемента сгенерированного массива указывается свойство описание \(`Description`\), которое начинается со слова "Search", далее ключевое слово, и в конце "on developer.chrome.com".

