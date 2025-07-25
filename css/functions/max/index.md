---
metaTitle: Функция max в CSS. Выбор наибольшего значения для гибкой вёрстки
metaDescription: Функция max в CSS. Выбор наибольшего значения для гибкой вёрстки
author: Дмитрий Нечаев
title: Функция max в CSS. Полное руководство с примерами
preview: Функция max в CSS позволяет выбрать наибольшее значение из двух или более заданных.
---

Функция `max()` в CSS позволяет выбрать наибольшее значение из двух или более заданных. Это полезный инструмент для создания гибких и адаптивных макетов, где размеры элементов должны динамически подстраиваться под условия, такие как размер экрана или контейнера. В этой статье мы подробно рассмотрим, как использовать функцию `max()`, её синтаксис и приведем практические примеры.

## Основные понятия

### Что такое функция `max()`?

Функция `max()` в CSS выбирает наибольшее значение из указанных. Она может принимать на вход несколько значений и возвращает самое большое из них. Это особенно полезно для задания минимальных размеров элементов, отступов и других свойств, которые должны адаптироваться в зависимости от контекста.

### Синтаксис

Синтаксис функции `max()` следующий:

```css
property: max(value1, value2, ...);

```

Где `property` — это CSS-свойство, а `value1`, `value2` и т.д. — это значения, из которых выбирается наибольшее.

## Примеры использования

### Адаптивные размеры

Функция `max()` позволяет создавать элементы, которые имеют минимальный размер, независимо от условий.

### Пример 1: Ограничение ширины элемента

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Пример max() - Ширина</title>
    <style>
        .container {
            width: 100%;
            max-width: 1200px;
            padding: 20px;
            box-sizing: border-box;
        }
        .content {
            width: max(300px, 50%); /* ширина не меньше 300px или 50% контейнера */
            background-color: lightblue;
            padding: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="content">Адаптивный контент</div>
    </div>
</body>
</html>

```

Использование функции `max()` в CSS открывает новые возможности для создания адаптивных и динамичных макетов, где размеры элементов зависят от различных условий. Однако, чтобы в полной мере использовать эту функцию, необходимо хорошо понимать принципы работы адаптивной верстки, а также особенности каскада и наследования стилей. Если вы хотите углубиться в эти темы и стать настоящим мастером адаптивного дизайна, приглашаем вас на наш курс [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=funktsiia-max-v-css-polnoe-rukovodstvo-s-primerami). На курсе 212 уроков и 19 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Сочетание разных единиц измерения

Функция `max()` позволяет комбинировать различные единицы измерения, такие как проценты, пиксели, em и другие.

### Пример 2: Высота элемента с минимальным ограничением

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Пример max() - Высота</title>
    <style>
        .box {
            height: max(100px, 20vh); /* высота не меньше 100px или 20% высоты окна */
            background-color: lightgreen;
        }
    </style>
</head>
<body>
    <div class="box">Адаптивная высота</div>
</body>
</html>

```

### Гибкие отступы и поля

Функция `max()` помогает задать отступы и поля, которые обеспечивают минимальные значения в зависимости от размера экрана.

### Пример 3: Адаптивные отступы

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Пример max() - Отступы</title>
    <style>
        .container {
            padding: max(10px, 2%); /* отступ не меньше 10px или 2% ширины окна */
            background-color: lightcoral;
        }
    </style>
</head>
<body>
    <div class="container">Адаптивные отступы</div>
</body>
</html>

```

### Создание сложных макетов

С помощью функции `max()` можно создавать сложные макеты, которые адаптируются к различным размерам экранов и контейнеров.

### Пример 4: Сложный макет с минимальной шириной и высотой

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Пример max() - Макет</title>
    <style>
        .sidebar {
            width: max(250px, 20%);
            float: left;
            background-color: lightgrey;
            height: 100vh;
        }
        .main {
            margin-left: max(250px, 20%);
            padding: 20px;
            background-color: lightyellow;
            height: 100vh;
        }
    </style>
</head>
<body>
    <div class="sidebar">Боковая панель</div>
    <div class="main">Основной контент</div>
</body>
</html>

```

## Поддержка браузеров

Функция `max()` поддерживается всеми современными браузерами, включая:

- Google Chrome
- Mozilla Firefox
- Safari
- Microsoft Edge
- Opera

## Заключение

Функция `max()` в CSS предоставляет гибкий и удобный способ для управления размерами элементов, отступами, полями и другими свойствами. Её использование особенно полезно для создания адаптивных и отзывчивых макетов, которые автоматически подстраиваются под размеры экрана или контейнера. Следуя приведенным выше примерам и рекомендациям, вы сможете эффективно применять `max()` в своих проектах и создавать более сложные и адаптивные дизайны.

Применение функции `max()` отлично сочетается с использованием Flexbox и Grid для создания сложных и адаптивных макетов. Чтобы получить комплексное понимание всех инструментов современной верстки и научиться создавать профессиональные веб-страницы, рекомендуем вам наш курс [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=funktsiia-max-v-css-polnoe-rukovodstvo-s-primerami). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир HTML и CSS прямо сегодня.
