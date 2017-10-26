#### Роль событий для этого компонента

Теперь перейдем к сценарию данного расширения. В нём используются слушатели `onInputStarted`, `onInputChanged`, `onInputEntered`, и `onInputCancelled`, которые относятся к `chrome.omnibox`. Так же данному компоненту не нужно указывать разрешения в файле манифесте. Код сценария указан в листинге 3-2.

![Рисунок 3-3. HelloOmniboxInput: Взаимодействие с omnibox](/assets/figure-3-3.png)

##### Рисунок 3-3. _HelloOmniboxInput: Взаимодействие с omnibox._




