### Адресная строка

Omnibox – это input компонент, который позволяет зарегистрировать ключевое слово для адресной строкой браузера. Чтобы использовать данный компонент нужен event сценарий, и соответствующие параметры в файле манифесте, как показано ниже:

```
"omnibox" : {
    "keyword" : "OI"
}
```

После указания параметра `omnibox`в манифесте, нужно задать атрибут `keyword`, значение которого не чувствительно к регистру. Если данные значение будет введено в адресной строке браузера, пользователь может начать взаимодействовать с расширением, как показано на рисунке 3-2 и 3-3.

![Рисунок 3-1. Менеджер расширений: HelloOmniboxInput](/assets/figure-3-1.png)

##### Рисунок 3-1. _Менеджер расширений: HelloOmniboxInput._

Для того чтобы использовать иконку в адресатной строке, вы можете её определить в свойстве icon файла манифеста \(листинг 3-1\). Обратите внимание, Google Chrome автоматически создают из 16 пиксельной иконки - черно-белую \(Листинг 3-1 и 3-2\). 

![Рисунок 3-2. HelloOmniboxInput: Ввод ключевого слова](/assets/figure-3-2.png)

##### Рисунок 3-2. _HelloOmniboxInput: Ввод ключевого слова._

##### Листинг 3-1. _Chapter3/HelloOmniboxInput/manifest.json_

```
{
    "manifest_version" : 2,
    "version" : "1.2",
    "name" : "HelloOmniboxInput",
    "description" : "Расширение демонстрирующее Omnibox",
    "background" : {
        "scripts" : ["event_script.js"],
        "persistent" : false
    },
    "omnibox" : {
        "keyword" : "OI"
    },
    "icons" : {
        "16" : "icon-16.png",
        "128" : "icon-128.png"
    }
}
```




