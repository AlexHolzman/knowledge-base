---
metaTitle: Number.isNaN() – JavaScript Numbers – Числа в JS
metaDescription: Как работает Number.isNaN() в JS | База знаний PurpleSchool
author: Дмитрий Фандорин
title: Number.isNaN() в JavaScript
preview: Метод Number.isNaN() - это встроенный метод JavaScript, который используется для определения, является ли переданное значение NaN (Not a Number)...
---

Метод Number.isNaN() - это встроенный метод JavaScript, который используется для определения, является ли переданное значение NaN (Not a Number). В этой статье мы рассмотрим, как использовать метод Number.isNaN() в JavaScript.

## Описание метода Number.isNaN()

Метод Number.isNaN() принимает один аргумент и возвращает логическое значение, указывающее, является ли переданное значение NaN. Если переданное значение не является NaN, метод вернет false. Если переданное значение является NaN, метод вернет true.

Например:

```javascript
console.log(Number.isNaN(NaN)); // true
console.log(Number.isNaN(42)); // false
console.log(Number.isNaN("42")); // false
console.log(Number.isNaN("hello")); // false
```

В первом примере мы передали значение NaN методу Number.isNaN() и получили результат true, что означает, что переданное значение является NaN.

Во втором примере мы передали число 42 методу Number.isNaN() и получили результат false, что означает, что переданное значение не является NaN.

В третьем примере мы передали строку "42" методу Number.isNaN() и получили результат false, что означает, что переданное значение не является NaN. Это произошло потому, что метод Number.isNaN() не преобразует строку в число перед проверкой, в отличие от глобальной функции isNaN().

В четвертом примере мы передали строку "hello" методу Number.isNaN() и получили результат false, что означает, что переданное значение не является NaN.

Функция `Number.isNaN()` позволяет определить, является ли значение `NaN` (Not-a-Number). Важно понимать разницу между `Number.isNaN()` и глобальной функцией `isNaN()`, чтобы избежать неожиданных результатов. Если вы хотите детальнее погрузиться в фундаментальные знания JavaScript, получить системное понимание языка и научиться применять его на практике — приходите на наш большой курс [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=number-isnan-v-javascript). На курсе 198 уроков и 30 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Как использовать метод Number.isNaN()

Использование метода Number.isNaN() довольно просто. Вы можете передать значение, которое хотите проверить на NaN, в качестве аргумента методу Number.isNaN(). Метод вернет true, если переданное значение является NaN, и false в противном случае.

```javascript
let x = NaN;
let y = "hello";
let z = 42;

console.log(Number.isNaN(x)); // true
console.log(Number.isNaN(y)); // false
console.log(Number.isNaN(z)); // false
```

В этом примере мы использовали метод Number.isNaN() для проверки переменных x, y и z на NaN. Переменная x содержит значение NaN, поэтому метод вернул true. Переменная y содержит строку "hello", которая не является NaN, поэтому метод вернул false. Переменная z содержит число 42, которое также не является NaN, поэтому метод вернул false.

## Заключение

Метод Number.isNaN() является полезным инструментом в JavaScript для проверки значений на NaN. Он обладает более точной логикой, чем глобальная функция isNaN(), и не преобразует значения в число перед проверкой. Если вы работаете с числами в JavaScript, метод Number.isNaN() может быть полезным для обработки ошибок и проверки ввода данных.

Использование `Number.isNaN()` позволяет точно определить, является ли значение `NaN`, избегая ложных срабатываний, которые могут возникнуть при использовании глобальной функции `isNaN()`. На курсе [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=number-isnan-v-javascript) вы изучите эту функцию и другие способы работы с числами и специальными значениями в JavaScript. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в JavaScript прямо сегодня.
