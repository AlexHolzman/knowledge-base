---
metaTitle: Метод then() в JavaScript
metaDescription: Разбираемся как использовать метод then() в JavaScript
author: Дмитрий Нечаев
title: Метод then() в JavaScript
preview: Учимся пользоваться методом then() в JavaScript. Разбираем примеры использования
---

В JavaScript для работы с асинхронными операциями часто используются промисы. Промис — это объект, который представляет собой завершение или неудачу асинхронной операции и её результат. Метод `.then()` является частью прототипа Promise и используется для планирования работы с успешным или ошибочным исходом промиса.

## Основы метода .then()

Метод `.then()` принимает два аргумента: функцию для обработки успешного исхода и функцию для обработки ошибки. Важно понимать, что метод `.then()` всегда возвращает новый промис, что позволяет строить цепочки промисов.

### Синтаксис

```jsx
promise.then(onFulfilled, onRejected);

```

- `onFulfilled` — функция, которая будет вызвана, если промис исполнится успешно. Эта функция имеет один аргумент, значение, с которым промис был выполнен.
- `onRejected` — функция, которая будет вызвана, если промис завершится с ошибкой. Этот параметр необязательный.

Метод `then()` является фундаментальным для работы с `Promise` в JavaScript. Он позволяет обрабатывать результат успешного выполнения или ошибку промиса. Понимание того, как правильно использовать `then()`, критически важно для написания асинхронного кода. Для тех, кто хочет получить более глубокие знания о работе с `Promise`, включая `async/await`, Event Loop и другие продвинутые концепции, настоятельно рекомендуем наш курс. Если вы хотите детальнее погрузиться в JavaScript — приходите на наш большой курс [JavaScript Advanced](https://purpleschool.ru/course/javascript-advanced?utm_source=knowledgebase&utm_medium=text&utm_campaign=metod-then-v-javascript). На курсе 196 уроков и 18 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Пример использования

Допустим, у нас есть функция, которая возвращает промис, разрешающийся с некоторым значением после 2 секунд:

```jsx
function resolveLater() {
    return new Promise((resolve) => {
        setTimeout(() => resolve("обещание выполнено"), 2000);
    });
}

```

Мы можем использовать `.then()` для обработки значения после выполнения промиса:

```jsx
resolveLater().then(value => {
    console.log(value);  // Выведет "обещание выполнено"
});

```

## Обработка ошибок

`.then()` также может принимать вторую функцию, которая будет вызвана, если промис будет отклонён:

```jsx
function rejectLater() {
    return new Promise((resolve, reject) => {
        setTimeout(() => reject(new Error("произошла ошибка")), 2000);
    });
}

rejectLater().then(
    value => console.log(value),
    error => console.error(error)  // Выведет "Error: произошла ошибка"
);

```

## Цепочка промисов

Одной из ключевых возможностей `.then()` является создание цепочек промисов, где результат одного промиса передаётся в другой:

```jsx
resolveLater()
    .then(value => {
        console.log(value);  // "обещание выполнено"
        return rejectLater();
    })
    .then(
        value => console.log(value),
        error => console.error(error)  // "Error: произошла ошибка"
    );

```

Это позволяет строить сложные асинхронные цепочки, где каждый следующий шаг зависит от результата предыдущего.

## Заключение

Метод `.then()` является мощным инструментом для работы с асинхронными операциями в JavaScript. Он позволяет обрабатывать результаты асинхронных операций удобным и читаемым способом, а также строить сложные цепочки асинхронных операций. Эффективное использование `.then()` может значительно упростить ваш код и сделать его более устойчивым к ошибкам.

Владение методом `then()` - это только начало пути в мир асинхронного JavaScript.  Чтобы создавать сложные и эффективные приложения, необходимо понимать принципы работы Event Loop, уметь использовать `async/await` и другие инструменты асинхронности.  Если вы хотите освоить все эти концепции на практике, рекомендуем вам курс [JavaScript Advanced](https://purpleschool.ru/course/javascript-advanced?utm_source=knowledgebase&utm_medium=text&utm_campaign=metod-then-v-javascript). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир продвинутого JavaScript прямо сегодня.
