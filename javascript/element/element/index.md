---
metaTitle: Элемент в JavaScript
metaDescription: Разбираемся как использовать элемент в JavaScript
author: Дмитрий Нечаев
title: Элемент в JavaScript
preview: Учимся пользоваться элементом в JavaScript. Разбираем примеры использования
---

В мире веб-разработки HTML и JavaScript тесно взаимосвязаны. Одним из ключевых аспектов этой связи является работа с HTML-элементами в коде JavaScript. В этой статье мы рассмотрим, как HTML-теги превращаются в объекты JavaScript, и как мы можем манипулировать ими в нашем коде.

## Получение элемента по идентификатору

Для начала давайте посмотрим, как можно получить доступ к HTML-элементам из JavaScript. Самый распространенный способ - использование идентификаторов элементов. Для этого мы используем метод `getElementById` объекта `document`.

```jsx
// Получаем элемент по его идентификатору
const myElement = document.getElementById('myElementId');

```

Здесь `myElementId` - это атрибут `id` элемента в HTML.

## Работа с HTML-содержимым элемента

Когда мы получаем элемент в JavaScript, мы можем получить доступ к его содержимому, атрибутам и другим свойствам. Давайте посмотрим, как это работает на примере изменения текстового содержимого элемента.

```html
<!-- HTML -->
<div id="myDiv">Пример текста</div>

```

```jsx
// JavaScript
const myDiv = document.getElementById('myDiv');
// Изменяем текстовое содержимое элемента
myDiv.textContent = 'Новый текст';

```

В результате выполнения этого кода текст внутри элемента `<div>` изменится на "Новый текст".

Элемент в JavaScript - это объект, представляющий HTML-элемент на веб-странице. Эти элементы составляют структуру веб-страницы и можно получать к ним доступ и манипулировать ими с помощью JavaScript. Если вы хотите понять как получить доступ к элементу в JavaScript и научится им управлять - приходите на наш большой курс [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=element-v-javascript). На курсе 198 уроков и 30 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Создание новых элементов

JavaScript также позволяет создавать новые HTML-элементы и добавлять их на страницу. Для этого мы используем метод `createElement` объекта `document`.

```jsx
// Создаем новый элемент <p>
const newParagraph = document.createElement('p');
// Устанавливаем текстовое содержимое
newParagraph.textContent = 'Новый абзац';
// Добавляем элемент в конец <body>
document.body.appendChild(newParagraph);

```

Теперь на странице будет добавлен новый абзац с текстом "Новый абзац".

## Обработка событий

JavaScript позволяет нам также назначать обработчики событий на HTML-элементы. Это позволяет реагировать на действия пользователя, такие как клики мышью или отправка форм.

```html
<!-- HTML -->
<button id="myButton">Нажми меня</button>

```

```jsx
// JavaScript
const myButton = document.getElementById('myButton');
// Назначаем обработчик события при клике на кнопку
myButton.addEventListener('click', () => {
  alert('Кнопка была нажата!');
});

```

Теперь при клике на кнопку появится всплывающее окно с сообщением "Кнопка была нажата!".

## Итоги

В этой статье мы рассмотрели основы работы с HTML-элементами в JavaScript. Мы узнали, как получать доступ к элементам, изменять их содержимое, создавать новые элементы и реагировать на события. Эти базовые концепции являются фундаментом для более сложных манипуляций с веб-страницей с использованием JavaScript.

Знание элементов JavaScript — основа разработки веб-страниц. Более глубокое понимание работы с DOM поможет в создании интерактивных приложений, в этом вам поможет наш курс [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=element-v-javascript). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир JavaScript прямо сегодня.
