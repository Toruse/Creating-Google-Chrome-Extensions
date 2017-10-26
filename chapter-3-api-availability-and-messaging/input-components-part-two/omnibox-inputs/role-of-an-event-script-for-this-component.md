#### Роль событий для этого компонента

Теперь перейдем к сценарию данного расширения. В нём используются слушатели `onInputStarted`, `onInputChanged`, `onInputEntered`, и `onInputCancelled`, которые относятся к `chrome.omnibox`. Так же данному компоненту не нужно указывать разрешения в файле манифесте. Код сценария указан в листинге 3-2.

![Рисунок 3-3. HelloOmniboxInput: Взаимодействие с omnibox](/assets/figure-3-3.png)

##### Рисунок 3-3. _HelloOmniboxInput: Взаимодействие с omnibox._

##### Листинг 3-2. _Chapter3/HelloOmniboxInput/event_script.js_

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
```

![Рисунок 3-4. HelloOmniboxInput: Похожие результаты](/assets/figure-3-4.png)

##### Рисунок 3-4. _HelloOmniboxInput: Похожие результаты._






