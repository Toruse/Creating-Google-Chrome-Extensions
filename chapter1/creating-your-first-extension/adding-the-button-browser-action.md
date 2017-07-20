### Добавляем кнопку: Browser-Action

Чтобы кнопка расширения отобразилась на панели инструментов браузера Google Chrome, нужно указать в манифесте атрибут _browser\_action_. Он имеет тип - объект \(то есть {}\), который включает в себя следующие свойства: _default\_title_, _default\_icon_, и _default\_popup_.

В листинге 1-1 показано, что каждое из этих свойств принимает строковое значение. Для всплывающей подсказки задается свойство _default\_title_. Свойство _default\_icon_ содержит путь к иконке в формате PNG, предназначенной для кнопки расширения Google Chrome, а свойство _default\_popup _указывается путь к HTML-файлу, который будет использоваться в качестве всплывающего окна.

##### Листинг 1-1. _ShowTime/manifest.json._

{

	"manifest\_version" : 2,

	"name" : "ShowTime",

	"description" : "Extension to show the current time and date",

	"version" : "1.2",

	"browser\_action": {

		"default\_title" : "ShowTime",

		"default\_icon" : "icon.png",

		"default\_popup" : "popup.html"

	},

	"icons" : {

		"16" : "icon16.png",

		"48" : "icon48.png",

		"128" : "icon128.png"

	}

}



