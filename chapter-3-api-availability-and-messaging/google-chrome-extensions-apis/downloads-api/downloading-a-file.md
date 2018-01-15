#### Загружаем файл

Для загрузки файла используется метод chrome.downloads.download, который принимает два параметра: options \(тип объект\) и callback \(тип функция\). В callback-функцию передается id или DownloadItem. Объект options содержит описание что скачать и как. Он поддерживает следующие свойства:

• url \(строка\)

• filename \(строка\)

• saveAs \(логическое значение\)

• method \(строка "GET" или "POST"\)

• headers \(массив\)

• body \(строка\)



Примечание:

Объект DownloadItem содержит множество важных свойств: id, filename, mime, startTime, endTime, bytesReceived и totalBytes \(более подробно о них можно почитать на странице https://developer.chrome.com/extensions/downloads\#type-DownloadItem\).

 

Обратите внимание, что свойства method, headers, и body используются если загрузка выполняется по протоколу HTTPS.

Теперь, рассмотрим пример использования метода download, для загрузки файла https://github.com/Apress/creating-google-chrome-extensions/archive/master.zip \(Листинг 3-25\).





