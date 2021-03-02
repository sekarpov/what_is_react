# Что такое React

### 1. Рендер страницы в JavaScript

Мы разделили рендеринг нашей страницы на отдельные компоненты, чтобы это было удобно обслуживать. А именно в нашем исходном коде мы разделили рендеринг страницы на отдельные функции, и теперь вызываем эти функции друг из друга. Например наша функция **Logo()** генерирует изображение со своими атрибутами и возвращает результат. А функция **Header()** генерирует шапку нашего сайта и в ней выводит создание логотипа.

После того как описали все компоненты мы вызываем функцию **App(state)** передавая **state** - текущее состояние, которое содержит все необходимые данные для отображения на странице. И эта функция App возвращает новое Dom дерево, которое мы теперь можем вставить в наш корневой элемент: 

```html
<div id="root"></div>
```

### 2. Динамика и иммутабельный flow

