#### Удаление закачанного

После загрузки файла, его возможно удалить используя метод `downloads.removeFile`. Он принимает два параметра `downloadId` и callback-функцию. 

Если нужно убрать загруженный файл из списка закачек, используйте метод `chrome.downloads.erase`, который принимает два параметра `query` и callback-функцию. Сам объект `query` содержит множество свойств, например: `id`, `startedBefore`, `startedAfter`, `endedBefore`, `endedAfter`, `filenameRegex`, и `urlRegex`. Описание данных свойств можно посмотреть на странице [https://developer.chrome.com/extensions/downloads\#method-erase](https://developer.chrome.com/extensions/downloads#method-erase).



