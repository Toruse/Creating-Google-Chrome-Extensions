#### Отмена или возобновление скачивания

После получения `id` или `DownloadItem` вы можете отменить, возобновить или приостановить загрузку. Для этого используются соответствующие методы:

* `chrome.downloads.cancel(integer downloadId, function callback)`
* `chrome.downloads.resume(integer downloadId, function callback)`
* `chrome.downloads.pause(integer downloadId, function callback)`



