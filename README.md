# Что такое React

### 1. Рендер страницы в JavaScript

Мы разделили рендеринг нашей страницы на отдельные компоненты, чтобы это было удобно обслуживать. А именно в нашем исходном коде мы разделили рендеринг страницы на отдельные функции, и теперь вызываем эти функции друг из друга. Например наша функция **Logo()** генерирует изображение со своими атрибутами и возвращает результат. А функция **Header()** генерирует шапку нашего сайта и в ней выводит создание логотипа.

После того как описали все компоненты мы вызываем функцию **App(state)** передавая **state** - текущее состояние, которое содержит все необходимые данные для отображения на странице. И эта функция App возвращает новое Dom дерево, которое мы теперь можем вставить в наш корневой элемент: 

```html
<div id="root"></div>
```

### 2. Динамика и иммутабельный flow

Добавили динамику, так чтобы на странице менялось время и цены. И в ходе добавления этой динамики мы пришли к работе с имутабельными компонентами. Т. е. вместо подхода с одноразовым запуском процедуры `render()` и последующим изменением DOM элементов напрямую, мы пришли к подходу с формированием одноразовых компонентов с перерендером всего приложения. Если на странице нужно что-то поменять (какие-либо данные), мы сначала меняем эти данные в нашем состоянии `state = {}` и после этого перезапускаем рендеринг `render(newDom, realDomRoot)` целиком нашего приложения. И каждый раз такой вызов рендера производит целиком подмену нашего приложения в браузере.

Проверяем в браузере - все работает. Такой подход удобен для разработки своей простотой, но у него есть 2 недостатка:
1.  **Сброс страницы**. 
     * Если попытаться выделить какой либо текст на странице, то видим что это выделение сразу сбрасывается. Потому что страница перерисовывается снова и снова на каждое изменение. 
    * И не можем проинспектировать элемент в средствах разработки, т.к. при раскрытии div он обратно сворачивается. 
    * Мы не можем интерактивно взаимодействовать с разными элементами на странице. Если будут например поля ввода на странице, то мы не можем в них ничего ввести, т.к. фокус курсора сбрасывается и тд.
2. **Производительность страницы**. 
    * При каждой вставке html кода в корневой элемент нашего документа, каждый раз браузер начинает расчитывать координаты и рисовать все эти элементы на экране. И если страница будет сложной из нескольких тыс div, то на каждые пол секунды такая полная перерисовака страницы будет сильно загружать процессор и видеокарту. Поэтому для сложных проектов этот способ не подходит.
    
### 3. Виртуальны DOM и синхронизация UI

