##### Добавление и удаление правил

Если вы желаете задекларировать правила для события onPageChanged, то используйте chrome.declarativeContent.onPageChanged.\*. Где \* может означать addRules или removeRules. Метод addRules принимает массив правил и callback-функцию.

```
var rule1 = {
    id : "some_rule_A", //Если не установлено свойство, оно будет создано
    priority : 100, //Опция, значение по умолчанию 100
    conditions : [/*условия*/],
    actions : [/*действия*/]
};
...
var ruleList = [rule1,rule2,...];
chrome.declarativeContent.onPageChanged.addRules(ruleList);
```


