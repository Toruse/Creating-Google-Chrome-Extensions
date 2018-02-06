## Создание темы для Google Chrome

Тема является особым видом расширения, которые меняют внешние оформление браузера. Они упакованы как обычные расширения, но без JavaScript сценариев и HTML-кода.

Вы можете попробовать темы из Chrome Web Store, перейдя по ссылке [https://chrome.google.com/webstore/category/themes](https://chrome.google.com/webstore/category/themes).

> **Примечание:**  
> Способ загрузки темы ничем не отличается от загрузки расширения.

Создать тему очень легко, для этого потребуется несколько изображений и сконфигурировать файл манифест. На рисунке 4-7 показаны изображения, которые будут использоваться в создаваемой теме, а в листинге 4-7 указан код файла манифеста.

##### Листинг 4-7. _Chapter4/Themes/manifest.json_

```
{
    "manifest_version" : 2,
    "name" : "HelloTheme",
    "version" : "1.2",
    "theme" : {
        "images" : {
            "theme_frame" : "images/theme_frame_golden.png", 
            "theme_toolbar" : "images/theme_toolbar_silver.png",
            "theme_ntp_background" : "images/theme_ntp_background.png",
            "theme_ntp_attribution" : "images/theme_ntp_attribution.png"
        },
        "colors" : {
            "tab_text" : [0,0,0],
            "ntp_text" : [255,255,255],
            "button_background" : [0,0,255] 
        },
        "tints" : { 
            "buttons" : [0.0,0.0,0.0],
            "frame" : [-1.0,-1.0,-1.0],
            "frame_inactive" : [-1.0,-1.0,0.3],
            "frame_incognito" : [-1.0,-1.0,0.2],
            "frame_incognito_inactive" : [-1.0,-1.0,0.0]
        }
    }
}
```

