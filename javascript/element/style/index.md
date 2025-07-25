---
metaTitle: .style в JavaScript
metaDescription: Разбираемся как использовать .style в JavaScript
author: Дмитрий Нечаев
title: .style в JavaScript
preview: Учимся пользоваться .style в JavaScript. Разбираем примеры использования
---

Свойство `.style` в JavaScript предоставляет возможность динамически изменять CSS-стили элементов напрямую из кода. Это полезно, когда нам нужно адаптировать внешний вид элементов в зависимости от различных условий или пользовательских действий. Давайте рассмотрим использование свойства `.style` более подробно с примерами.

## Введение в `.style`

Свойство `.style` представляет собой объект, который содержит все инлайновые стили элемента. Он позволяет нам добавлять, изменять и удалять CSS-стили элемента непосредственно из JavaScript, что делает его мощным инструментом для динамического управления внешним видом страницы.

## Примеры использования `.style`

Давайте рассмотрим несколько примеров использования свойства `.style` для изменения CSS-стилей элементов.

### 1. Изменение цвета фона элемента

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Пример</title>
</head>
<body>
  <div id="myElement">Это элемент</div>

  <script>
    // Получаем ссылку на элемент
    const element = document.getElementById('myElement');

    // Изменяем цвет фона элемента
    element.style.backgroundColor = 'lightblue';
  </script>
</body>
</html>

```

В этом примере мы изменяем цвет фона элемента с помощью свойства `.style.backgroundColor`.

Динамическое изменение стилей элементов — мощный инструмент для создания интерактивных и адаптивных веб-страниц. Свойство `.style` позволяет получать доступ к стилям элемента и изменять их непосредственно из JavaScript. Если вы хотите детальнее погрузиться в мир CSS-in-JS, научиться управлять стилями элементов динамически, анимировать элементы и создавать сложные интерфейсы — приходите на наш большой курс [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=style-v-javascript). На курсе 198 уроков и 30 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### 2. Изменение размера шрифта и цвета текста

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Пример</title>
</head>
<body>
  <p id="myText">Это текст</p>

  <script>
    // Получаем ссылку на элемент
    const text = document.getElementById('myText');

    // Изменяем размер шрифта и цвет текста
    text.style.fontSize = '20px';
    text.style.color = 'red';
  </script>
</body>
</html>

```

В этом примере мы изменяем размер шрифта и цвет текста элемента с помощью свойств `.style.fontSize` и `.style.color`.

### 3. Изменение отступов и позиционирование элемента

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Пример</title>
  <style>
    #myBox {
      width: 100px;
      height: 100px;
      background-color: lightgreen;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div id="myBox">Это блок</div>

  <script>
    // Получаем ссылку на элемент
    const box = document.getElementById('myBox');

    // Изменяем отступ сверху и позиционирование элемента
    box.style.marginTop = '50px';
    box.style.position = 'relative';
    box.style.left = '50px';
  </script>
</body>
</html>

```

В этом примере мы изменяем отступ сверху и позиционирование элемента с помощью свойств `.style.marginTop`, `.style.position` и `.style.left`.

## Заключение

Свойство `.style` в JavaScript предоставляет простой и эффективный способ изменять CSS-стили элементов непосредственно из кода. Это помогает создавать динамические и адаптивные пользовательские интерфейсы, а также делает код более модульным и управляемым. Надеюсь, данная статья помогла вам лучше понять, как использовать `.style` в ваших проектах JavaScript.

Хотя свойство `.style` предоставляет быстрый способ изменения стилей, существуют и другие, более мощные методы, такие как работа с классами CSS и использование CSS-переменных. Для полного понимания возможностей стилизации веб-страниц с помощью JavaScript, мы рекомендуем наш курс [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=style-v-javascript). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир JavaScript прямо сегодня.
