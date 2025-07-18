---
metaTitle: Управление анимацией с помощью CSS animation-timing-function
metaDescription: Узнайте, как с помощью свойства CSS animation-timing-function управлять механизмом проигрывания анимаций; скачками, плавно или как прыгающий мячик. Полное руководство с примерами.
author: Дмитрий Нечаев
title: CSS animation-timing-function; Полное руководство по управлению проигрыванием анимаций
preview: Узнайте, как использовать CSS animation-timing-function для управления проигрыванием анимаций. Полное руководство с примерами.
---

Свойство `animation-timing-function` в CSS позволяет управлять механизмом проигрывания анимаций, определяя, как будет изменяться скорость анимации на протяжении её выполнения. С его помощью можно задавать плавные переходы, скачки или создавать эффект прыгающего мячика. В этой статье мы подробно рассмотрим, как использовать `animation-timing-function`, и приведем примеры для лучшего понимания.

## Основы animation-timing-function

Свойство `animation-timing-function` определяет распределение скорости анимации на её протяжении. Это влияет на то, как анимация будет выглядеть и ощущаться при воспроизведении.

### Варианты значения animation-timing-function

- `ease` - Анимация начинается медленно, ускоряется и снова замедляется к концу (по умолчанию).
- `linear` - Анимация выполняется с постоянной скоростью от начала до конца.
- `ease-in` - Анимация начинается медленно и ускоряется к концу.
- `ease-out` - Анимация начинается быстро и замедляется к концу.
- `ease-in-out` - Анимация начинается медленно, ускоряется и снова замедляется к концу.
- `cubic-bezier(n,n,n,n)` - Пользовательская функция Безье для точного контроля анимации.
- `steps(number, start|end)` - Анимация выполняется в виде шагов.

`animation-timing-function` позволяет контролировать скорость изменения свойств во время анимации. Вы можете создавать плавные, резкие, линейные и другие виды анимаций. Чтобы создавать действительно интересные и привлекательные анимации, необходимо понимать, как работают разные значения `animation-timing-function`. Если вы хотите детальнее погрузиться в мир веб-анимации и научиться создавать красивые и динамичные анимации с помощью CSS — приходите на наш большой курс [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=css-animation-timing-function-polnoe-rukovodstvo-po-upravleniyu-proigryvaniem-animatsiy). На курсе 212 уроков и 19 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Синтаксис animation-timing-function

Синтаксис использования свойства `animation-timing-function` простой:

```css
.element {
  animation-timing-function: значение;
}
```

### Пример использования

Рассмотрим пример, где анимация перемещения элемента воспроизводится с разными функциями времени:

```css
@keyframes move {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(100px);
  }
}

.ease-element {
  animation-name: move;
  animation-duration: 2s;
  animation-timing-function: ease; /* Плавное начало и конец */
}

.linear-element {
  animation-name: move;
  animation-duration: 2s;
  animation-timing-function: linear; /* Постоянная скорость */
}

.ease-in-element {
  animation-name: move;
  animation-duration: 2s;
  animation-timing-function: ease-in; /* Медленный старт */
}

.ease-out-element {
  animation-name: move;
  animation-duration: 2s;
  animation-timing-function: ease-out; /* Медленный конец */
}

.ease-in-out-element {
  animation-name: move;
  animation-duration: 2s;
  animation-timing-function: ease-in-out; /* Медленный старт и конец */
}
```

## Пользовательская функция Безье

Для более точного контроля анимации можно использовать функцию Безье с четырьмя параметрами, которые определяют форму кривой.

### Пример с функцией Безье

```css
@keyframes bounce {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(-100px);
  }
}

.bezier-element {
  animation-name: bounce;
  animation-duration: 1s;
  animation-timing-function: cubic-bezier(0.68, -0.55, 0.27, 1.55); /* Эффект прыжка */
  animation-iteration-count: infinite;
}
```

## Шаговая функция steps

С помощью функции `steps` можно создавать анимации, которые выполняются в виде дискретных шагов.

### Пример с шаговой функцией

```css
@keyframes slide {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(100px);
  }
}

.steps-element {
  animation-name: slide;
  animation-duration: 2s;
  animation-timing-function: steps(5, end); /* Анимация в 5 шагов */
}
```

## Комбинирование с другими свойствами анимации

Свойство `animation-timing-function` часто используется вместе с другими анимационными свойствами, такими как `animation-duration`, `animation-delay`, `animation-iteration-count`, и `animation-direction`.

### Пример с комплексной анимацией

Рассмотрим более сложный пример, где используется несколько анимационных свойств:

```css
@keyframes complex {
  0% {
    transform: translateX(0) scale(1);
  }
  50% {
    transform: translateX(50px) scale(1.5);
  }
  100% {
    transform: translateX(100px) scale(1);
  }
}

.complex-element {
  animation-name: complex;
  animation-duration: 3s;
  animation-timing-function: ease-in-out; /* Плавный старт и конец */
  animation-delay: 0.5s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```

## Советы и рекомендации

1. **Выбор подходящей функции времени**. Подбирайте функцию времени в зависимости от характера анимации. Например, для плавных движений лучше использовать `ease`, а для постоянной скорости - `linear`.

2. **Использование пользовательских функций Безье**. Для создания уникальных и сложных анимаций используйте `cubic-bezier`, чтобы точно настроить динамику анимации.

3. **Тестирование в разных браузерах**. Убедитесь, что ваши анимации корректно работают в различных браузерах, так как поддержка CSS-анимаций может отличаться.

## Заключение

Свойство `animation-timing-function` в CSS является мощным инструментом для управления проигрыванием анимаций. С его помощью можно задавать различные эффекты скорости и динамики анимаций, делая их более реалистичными и привлекательными. Следуя приведенным рекомендациям и примерам, вы сможете эффективно использовать `animation-timing-function` в своих проектах, улучшая взаимодействие с пользователями и делая ваши веб-страницы более интересными и интерактивными.

Правильный выбор `animation-timing-function` может значительно улучшить впечатление от анимации. Но для создания действительно запоминающихся анимаций необходимо не только знать, как работает `animation-timing-function`, но и обладать хорошим чувством стиля и пониманием принципов анимации. На нашем курсе [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=css-animation-timing-function-polnoe-rukovodstvo-po-upravleniyu-proigryvaniem-animatsiy) вы научитесь создавать профессиональные веб-сайты с красивой и динамичной анимацией. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир HTML и CSS прямо сегодня.
