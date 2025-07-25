---
metaTitle: Полное руководство по свойству transform в CSS
metaDescription: Узнайте, как использовать свойство transform в CSS для поворота, искажения и изменения масштаба элементов. Подробное руководство с примерами.
author: Дмитрий Нечаев
title: Управление элементами с помощью свойства transform в CSS
preview: Откройте для себя возможности свойства transform в CSS; поворот, искажение и изменение масштаба элементов. Примеры и советы по применению.
---

Свойство `transform` в CSS открывает множество возможностей для манипуляций с элементами на веб-странице. С его помощью можно поворачивать, изменять масштаб, искажать и перемещать элементы, создавая удивительные визуальные эффекты. В этой статье мы рассмотрим все основные аспекты использования свойства `transform` и приведем примеры для каждого из них.

**Что такое transform?**

Свойство `transform` в CSS позволяет применять двумерные и трехмерные преобразования к элементам. С его помощью можно поворачивать, масштабировать, перемещать и искажать элементы.

**Синтаксис**

```css
transform: none | transform-function;
```

Значение `none` отменяет любые ранее примененные преобразования. `transform-function` может быть одной из следующих функций или их комбинацией.

Свойство `transform` - это основа для создания анимированных эффектов и интерактивных элементов на веб-странице. Для создания крутых проектов необходимо знать другие свойства CSS. Если вы хотите детальнее погрузиться в тонкости веб-дизайна — приходите на наш большой курс [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=upravlenie-elementami-s-pomoshchyu-svoystva-transform-v-css). На курсе 212 уроков и 19 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

**Основные функции transform**

1. **translate()**: Перемещает элемент.
   - `translate(x, y)`: Перемещает элемент по оси X на значение `x` и по оси Y на значение `y`.
   - Пример:
     ```css
     .translate {
         transform: translate(50px, 100px);
     }
     ```

2. **rotate()**: Поворачивает элемент.
   - `rotate(angle)`: Поворачивает элемент на угол `angle`.
   - Пример:
     ```css
     .rotate {
         transform: rotate(45deg);
     }
     ```

3. **scale()**: Изменяет масштаб элемента.
   - `scale(x, y)`: Изменяет масштаб элемента по оси X на значение `x` и по оси Y на значение `y`.
   - Пример:
     ```css
     .scale {
         transform: scale(1.5, 0.5);
     }
     ```

4. **skew()**: Искажает элемент.
   - `skew(x-angle, y-angle)`: Искажает элемент на угол `x-angle` по оси X и `y-angle` по оси Y.
   - Пример:
     ```css
     .skew {
         transform: skew(30deg, 20deg);
     }
     ```

**Комбинирование функций**

Вы можете комбинировать несколько функций `transform` для создания сложных эффектов. Например, комбинирование поворота и масштабирования:

```css
.combined {
    transform: rotate(45deg) scale(1.5);
}
```

**Пример использования**

Рассмотрим пример, в котором мы применяем несколько функций `transform` к разным элементам:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Transform Example</title>
    <style>
        .box {
            width: 100px;
            height: 100px;
            background-color: red;
            margin: 20px;
            display: inline-block;
        }

        .translate {
            transform: translate(50px, 50px);
        }

        .rotate {
            transform: rotate(45deg);
        }

        .scale {
            transform: scale(1.5);
        }

        .skew {
            transform: skew(20deg);
        }

        .combined {
            transform: translate(30px, 30px) rotate(30deg) scale(0.8) skew(10deg, 15deg);
        }
    </style>
</head>
<body>
    <div class="box translate"></div>
    <div class="box rotate"></div>
    <div class="box scale"></div>
    <div class="box skew"></div>
    <div class="box combined"></div>
</body>
</html>
```

В этом примере у нас есть пять квадратов, каждый из которых демонстрирует разные преобразования с помощью свойства `transform`.

**Трехмерные преобразования**

CSS также поддерживает трехмерные преобразования, такие как `rotateX()`, `rotateY()`, `rotateZ()`, `translateZ()`, `scaleZ()`, и `perspective()`.

**Пример трехмерного преобразования**

```css
.threeD {
    transform: rotateX(45deg) rotateY(45deg);
    perspective: 500px;
}
```

**Заключение**

Свойство `transform` в CSS предоставляет мощный и гибкий инструмент для создания визуально привлекательных и сложных эффектов. Оно позволяет легко поворачивать, изменять масштаб, перемещать и искажать элементы, открывая перед разработчиками огромные возможности для творчества. Надеюсь, это руководство помогло вам понять, как использовать `transform` в ваших проектах.

Управление элементами с помощью свойства `transform` является важным навыком. Расширьте свои знания, чтобы создавать классные веб-страницы. Начните свое обучение с нашим курсом [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=upravlenie-elementami-s-pomoshchyu-svoystva-transform-v-css). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир HTML и CSS прямо сегодня.
