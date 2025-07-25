---
metaTitle: Управление анимациями с помощью transition-timing-function в CSS
metaDescription: Узнайте, как использовать transition-timing-function в CSS для создания плавных и причудливых анимаций. Полное руководство с примерами.
author: Дмитрий Нечаев
title: Полное руководство по transition-timing-function в CSS
preview: Откройте для себя возможности transition-timing-function в CSS для создания уникальных анимаций. Примеры и советы по применению.
---

В CSS свойство `transition-timing-function` играет ключевую роль в управлении тем, как элемент будет меняться во времени. Оно определяет характер изменения значения анимируемого свойства, будь то линейный переход или более сложная кривая. В этой статье мы подробно рассмотрим все возможности `transition-timing-function`, его значения и примеры использования.

**Что такое transition-timing-function?**

Свойство `transition-timing-function` в CSS определяет функцию времени для перехода. Оно управляет темпом изменения свойства на протяжении всего перехода, задавая, как быстро или медленно произойдет изменение на разных этапах анимации.

`transition-timing-function` позволяет управлять скоростью изменения свойств во время transition. Вы можете создавать плавные, резкие, причудливые и другие виды анимаций. Чтобы создавать действительно впечатляющие переходы, необходимо хорошо понимать, как работают различные значения `transition-timing-function` и как их комбинировать. Если вы хотите детальнее погрузиться в мир CSS-анимаций и научиться создавать плавные и причудливые анимации — приходите на наш большой курс [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=polnoe-rukovodstvo-po-transition-timing-function-v-css). На курсе 212 уроков и 19 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

**Синтаксис**

```css
transition-timing-function: значение;
```

Значение может быть одним из предопределенных ключевых слов или функцией bezier-кривой.

**Предопределенные значения**

1. `linear`: Переход происходит с постоянной скоростью.
2. `ease`: Переход начинается медленно, затем ускоряется и снова замедляется к концу.
3. `ease-in`: Переход начинается медленно и ускоряется к концу.
4. `ease-out`: Переход начинается быстро и замедляется к концу.
5. `ease-in-out`: Переход начинается медленно, затем ускоряется и снова замедляется к концу.

**Пример использования**

Рассмотрим простой пример, где квадрат изменяет размер с различными функциями времени:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Transition Timing Function Example</title>
    <style>
        .box {
            width: 100px;
            height: 100px;
            background-color: red;
            margin: 20px;
            transition-property: width, height;
            transition-duration: 2s;
        }

        .linear {
            transition-timing-function: linear;
        }

        .ease {
            transition-timing-function: ease;
        }

        .ease-in {
            transition-timing-function: ease-in;
        }

        .ease-out {
            transition-timing-function: ease-out;
        }

        .ease-in-out {
            transition-timing-function: ease-in-out;
        }

        .box:hover {
            width: 200px;
            height: 200px;
        }
    </style>
</head>
<body>
    <div class="box linear"></div>
    <div class="box ease"></div>
    <div class="box ease-in"></div>
    <div class="box ease-out"></div>
    <div class="box ease-in-out"></div>
</body>
</html>
```

В этом примере мы видим пять квадратов, каждый из которых использует разные функции времени для анимации изменения размера при наведении курсора.

**Кубические bezier-кривые**

Для более точного контроля за анимацией можно использовать кубические bezier-кривые. Синтаксис такой:

```css
transition-timing-function: cubic-bezier(x1, y1, x2, y2);
```

Где `x1`, `y1`, `x2` и `y2` — контрольные точки кривой, определяющие ее форму. Вот пример использования cubic-bezier:

```css
.custom-timing {
    transition-timing-function: cubic-bezier(0.68, -0.55, 0.27, 1.55);
}
```

**Пример использования cubic-bezier**

Добавим к нашему примеру еще один квадрат с нестандартной функцией времени:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Custom Timing Function Example</title>
    <style>
        .box.custom {
            transition-timing-function: cubic-bezier(0.68, -0.55, 0.27, 1.55);
        }

        .box:hover {
            width: 200px;
            height: 200px;
        }
    </style>
</head>
<body>
    <div class="box custom"></div>
</body>
</html>
```

В этом примере квадрат будет изменять размер с эффектом "упругости" благодаря заданным контрольным точкам bezier-кривой.

**Шаговые функции**

Еще один интересный способ управления анимациями — шаговые функции. Используйте `steps(количество_шагов, направление)`, чтобы разделить анимацию на определенные шаги.

```css
.transition-steps {
    transition-timing-function: steps(4, end);
}
```

**Пример использования steps**

Рассмотрим пример с квадратом, который изменяет размер в четыре шага:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Steps Timing Function Example</title>
    <style>
        .box.steps {
            transition-timing-function: steps(4, end);
        }

        .box:hover {
            width: 200px;
            height: 200px;
        }
    </style>
</head>
<body>
    <div class="box steps"></div>
</body>
</html>
```

В этом примере размер квадрата изменится в четыре дискретных шага.

**Заключение**

Свойство `transition-timing-function` в CSS предоставляет широкие возможности для управления анимациями, позволяя создавать как простые линейные переходы, так и сложные, причудливые эффекты. Использование предопределенных значений, кубических bezier-кривых и шаговых функций позволяет достичь нужного визуального эффекта и сделать интерфейсы более привлекательными и интерактивными. Надеюсь, это руководство помогло вам понять, как использовать `transition-timing-function` в ваших проектах.

Правильное использование `transition-timing-function` может значительно улучшить пользовательский опыт. Но для создания действительно впечатляющих анимаций необходимо не только знать, как работает `transition-timing-function`, но и обладать хорошим чувством стиля и пониманием принципов анимации. На нашем курсе [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=polnoe-rukovodstvo-po-transition-timing-function-v-css) вы научитесь создавать профессиональные веб-сайты с плавной и красивой анимацией. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир HTML и CSS прямо сегодня.
