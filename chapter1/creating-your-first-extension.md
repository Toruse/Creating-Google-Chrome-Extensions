## Пишем первое расширение

Первое расширение, которое вы разработает, будет называется `ShowTime`. Оно добавлять кнопку на панель инструментов Google Chrome. При нажатии на неё откроется всплывающее окно \(Рисунок 1-8\), где отобразиться текущее время и дата.

![Рисунок 1-8. Всплывающее окно расширения при нажатии на кнопку панели инструментов.](/assets/figure-1-8.png)

##### Рисунок 1-8. _Всплывающее окно расширения при нажатии на кнопку в панели инструментов._

> **Примечание:**  
> Manifest.json - это зарезервированное имя файла в расширении. Все остальные файлы могут называться как угодно.

Для начала, нужно создать папку со следующими файлами: popup.html, popup\_script.js, icon.png, и manifest.json \(Рисунок 1-9\).

![Рисунок 1-9. Файлы расширения ShowTime.](/assets/figure-1-9.png)

##### Рисунок 1-9. _Файлы расширения ShowTime._

Файл HTML будет содержать разметку всплывающего окна нашего расширения. Файл JavaScript будет содержать логику приложения \(в данном случае код для отображения текущего времени и даты\). Файл манифеста будет вмешать информацию о расширение. Файл изображения icon.png предназначен для кнопки на панели инструментов браузера \(Рисунок 1-10\).

![Рисунок 1-10. Кнопка расширения на панели инструментов Google Chrome.](/assets/figure-1-10.png)

##### Рисунок 1-10. _Кнопка расширения на панели инструментов Google Chrome._

