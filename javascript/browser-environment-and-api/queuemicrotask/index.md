---
metaTitle: queueMicrotask() – JavaScript Browser Environment And API – Браузерное окружение и API в JS
metaDescription: Как работает queueMicrotask() в JS | База знаний PurpleSchool
author: Дмитрий Фандорин
title: queueMicrotask() в JavaScript
preview: queueMicrotask() - это функция в JavaScript, которая используется для добавления задачи в микроочередь...
---

queueMicrotask() - это функция в JavaScript, которая используется для добавления задачи в микроочередь. Это позволяет выполнять задачи в следующей микротаске, после завершения текущей таски.

## Форма записи

Функция queueMicrotask() вызывается с одним аргументом - функцией, которая будет добавлена в микроочередь.

Пример:

```javascript
queueMicrotask(() => {
  console.log('Эта задача будет выполнена в следующей микротаске');
});
```

## Описание работы

Функция queueMicrotask() позволяет добавлять задачи в микроочередь. Микроочередь - это очередь задач, которые будут выполнены в следующей микротаске, после завершения текущей таски.

Добавление задачи в микроочередь с помощью функции queueMicrotask() позволяет гарантировать, что эта задача будет выполнена в следующей микротаске, даже если текущая таска займет длительное время.

`queueMicrotask()` позволяет запланировать выполнение функции в микрозадаче, которая будет выполнена после текущей макрозадачи.  Это мощный инструмент для управления асинхронностью и обеспечения оптимальной производительности. Чтобы полностью разобраться в механизмах асинхронности JavaScript и понять, как работает `queueMicrotask()`, важно иметь хорошее понимание основ языка. Если вы хотите получить прочный фундамент в JavaScript и узнать, как работают асинхронные операции, приходите на наш большой курс [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=queuemicrotask-v-javascript). На курсе 198 уроков и 30 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Пример

Пример использования функции queueMicrotask():

```javascript
function doSomething() {
  console.log('Начало выполнения функции');
  queueMicrotask(() => {
    console.log('Задача в микроочереди');
  });
  console.log('Окончание выполнения функции');
}

doSomething();
```

Этот код добавит задачу в микроочередь и выведет в консоль сообщения о начале и окончании выполнения функции, а также сообщение из задачи, добавленной в микроочередь.

## Заключение

Функция queueMicrotask() - это удобный способ добавления задач в микроочередь. Использование микроочереди позволяет гарантировать, что задачи будут выполнены в следующей микротаске, даже если текущая таска займет длительное время. Это может помочь избежать задержек в выполнении программы и повысить ее производительность.

Подводя итоги, `queueMicrotask()` - это продвинутый инструмент для тонкой настройки асинхронного поведения. Для более глубокого понимания асинхронности, event loop и микрозадач, рассмотрите курс [JavaScript Advanced](https://purpleschool.ru/course/javascript-advanced?utm_source=knowledgebase&utm_medium=text&utm_campaign=queuemicrotask-v-javascript). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир продвинутого JavaScript прямо сегодня.
