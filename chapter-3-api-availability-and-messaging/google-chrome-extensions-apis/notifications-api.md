### Notifications API

При помощи `chrome.notifications` API можно создать гибкие уведомления для пользователей в системном лотке \(tray\) операционной системы. Пример использования показан в листинге 3-27.

##### Листинг 3-27. _Chapter3/NotificationsAPI/event\_script.js_

```
//region {переменные и функции}
var greeting = "Hello World!";
var title = "NotificationsAPI";
var message = "Test message X";
var oneMinuteAsMilliseconds = 1 * 60 * 1000;
//getTime возвращает количество миллисекунд, прошедших с полуночи 1 января 1970 года GMT
var currentTimeAsMilliseconds = new Date().getTime();
var notificationId = "myNotification1";
var NOTIFICATION_TEMPLATE_TYPE = {
    BASIC : "basic",
    IMAGE : "image",
    LIST : "list",
    PROGRESS : "progress"
};
var myButton1 = {
    title : "Click X",
    iconUrl : "button.png"
};
var myButton2 = {
    title : "Click Y",
    iconUrl : "button.png"
};
var myItem1 = {
    title : "Item X",
    message : "This is item X"
};
var myItem2 = {
    title : "Item Y",
    message : "This is item Y"
};
var notificationOptions = {
    type : NOTIFICATION_TEMPLATE_TYPE.LIST,
    iconUrl : "icon.png",
    title : title,
    message : message,
    /*eventTime : currentTimeAsMilliseconds + oneMinuteAsMilliseconds,*/
    buttons : [myButton1,myButton2],
    /*imageUrl : "icon.png",*/
    items : [myItem1,myItem2], //comment out for BASIC
    /*progress : 0,*/
    isClickable : true
};
//end-region

//region {вычисления}
console.log(greeting);
chrome.notifications.create(notificationId,notificationOptions,function(id) {
    console.log("create: " + id);
});
/*
chrome.notifications.clear(notificationId,function(wasCleared) {
    console.log("clear: " + wasCleared);
});
*/
/*
chrome.notifications.getAll(function(notifications) {
    console.log("getAll:");
    console.log(notifications);
});
*/
chrome.notifications.onClicked.addListener(function(id) { //notification-id
    console.log("onClicked: " + id);
    notificationOptions.title = title + " (onClicked)";
    chrome.notifications.update(notificationId,notificationOptions,function(wasUpdated) {
        console.log("update: " + wasUpdated);
    });
});
chrome.notifications.onClosed.addListener(function(notificationId,byUser) {
    console.log("onClosed: " + notificationId);
});
chrome.notifications.onButtonClicked.addListener(function(notificationId,buttonIndex) {
    console.log("onButtonClicked: " + buttonIndex);
});
```



