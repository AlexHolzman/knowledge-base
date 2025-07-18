---
metaTitle: substring() – JavaScript String – Методы строк в JS
metaDescription: Как работает метод substring() в JavaScript. Всё о методах работы со строками в JavaScript | База знаний PurpleSchool
author: Виталий Котов
title: Как работает метод substring() - JavaScript
preview: Метод substring() возвращает заданную часть строки между начальным и конечным индексами...
---

Метод `substring()` возвращает заданную часть строки между начальным и конечным индексами.

```javascript
const message = "JavaScript is fun.";

// получить подстроку, начиная с индекса 0 до 10
let result = message.substring(0, 10);
console.log(result);

// Выавод в консоль: JavaScript
```

## Синтаксис substring()

Синтаксис метода `substring()` следующий:

```javascript
str.substring(indexStart, indexEnd);
```

Где `str` - это строка.

Метод `substring()` извлекает часть строки между двумя указанными индексами. Это важный инструмент для обработки текста и извлечения необходимых фрагментов. Чтобы эффективно использовать `substring()` и другие методы работы со строками, необходимо понимать их особенности и принципы работы. Если вы хотите детальнее погрузиться в особенности работы со строками в JavaScript — приходите на наш большой курс [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=kak-rabotaet-metod-substring-v-javascript). На курсе 198 уроков и 30 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Параметры substring()

Метод `substring()` принимает:

- `indexStart` - индекс первого символа, с которого следует начать включение в возвращаемую подстроку.
- `indexEnd` (необязательно) - индекс, перед которым следует остановить извлечение. (Исключительно) Если опущено, то извлечение будет производиться до конца строки.

> **Примечание:**
>
> - Любое **значение аргумента < 0** воспринимается как **0**.
> - Любое **значение аргумента > str.length** рассматривается как **str.length**.
> - Любое значение аргумента `NaN` воспринимается как **0**.
> - Если `indexStart` больше `indexEnd`, два аргумента меняются местами, т.е. `str.substring(a, b)` будет `str.substring(b, a)`.

## Возвращаемое значение substring()

Возвращает новую строку, содержащую указанную часть заданной строки.

> **Примечание:** substring() не изменяет исходную строку.

## Примеры

### Пример 1: Использование метода substring()

```javascript
let string = "Purpleschool JavaScript Tutorials";

// первый символ
substr1 = string.substring(0, 1);
console.log(substr1); // P

// если начало > конца, они меняются местами
substr2 = string.substring(1, 0);
console.log(substr2); // P

// С 14-го до последнего символа
substr3 = string.substring(13);
console.log(substr3); // JavaScript Tutorials

// крайними значениями являются 0 и str.length

// то же, что и string.substring(0)
substr4 = string.substring(-44, 90);
console.log(substr4); // Purpleschool JavaScript Tutorials

substr5 = string.substring(0, string.length - 1);
console.log(substr5); // Purpleschool JavaScript Tutorial
```

Вывод в консоль:

```
P
P
ol JavaScript Tutorials
Purpleschool JavaScript Tutorials
Purpleschool JavaScript Tutorial
```

### Пример 2: Замена подстроки в строке

```javascript
// Заменяет старые символы новыми символами в строке
function replaceString(oldChars, newChars, string) {
  for (let i = 0; i < string.length; ++i) {
    if (string.substring(i, i + oldChars.length) == oldChars) {
      string =
        string.substring(0, i) +
        newChars +
        string.substring(i + oldChars.length, string.length);
    }
  }
  return string;
}

const string = "Java Tutorials";
let newString = replaceString("Java", "JavaScript", string);
console.log(newString); // JavaScript Tutorials
```

Вывод в консоль:

```
JavaScript Tutorials
```

Освоив метод `substring()`, вы сделали важный шаг к мастерству работы со строками. Но на этом пути вас ждет еще много интересного. Чтобы уверенно разрабатывать современные веб-приложения, вам потребуется глубокое понимание JavaScript, включая работу с массивами, объектами и DOM. На курсе [JavaScript с нуля](https://purpleschool.ru/course/javascript-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=kak-rabotaet-metod-substring-v-javascript) вы найдете все необходимое для построения прочного фундамента знаний. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в JavaScript прямо сегодня.
