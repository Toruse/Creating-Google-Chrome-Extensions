### Компоненты Browser-Action и Page-Action

Компоненты Browser-Action и Page-Action - это кнопки на панели инструментов Google Chrome, как показано на рисунке 2-1. Browser-Action находится справа за адресной строкой, а Page-Action находится внутри адресной строки с правой стороны. Само расширение может использовать только один из компонентов Browser-Action или Page-Action.

Browser-Action и Page-Action соответственно имеет своё собственное название, иконку, кнопку, и Popup окно. Все эти параметры указываются в манифесте. Для доступа к данным компонентам из сценариев расширения предоставляет API для Browser-Action - это `chrome.browserAction`, а для Page-Action - `chrome.pageAction`.

