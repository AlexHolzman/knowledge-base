---
metaTitle: Использование transition во Vue
metaDescription: Научитесь плавно анимировать элементы в Vue - разбираем transition, кастомные классы, работу с видимостью и оптимизацию производительности
author: Олег Марков
title: Использование transition во Vue
preview: Узнайте, как использовать transition во Vue для создания плавных анимаций элементов - подберите нужные классы, скомбинируйте переходы и применяйте их к реальным задачам
---

## Введение

Веб-приложения должны быть не только функциональными, но и отзывчивыми для пользователя. Анимации и плавные переходы делают интерфейсы более приятными и современными. В экосистеме Vue для этого предусмотрен специальный способ — компонент `<transition>`, который помогает вам создавать анимированное появление, исчезновение и изменение состояния DOM-элементов и компонентов.

В этой статье я расскажу, как использовать `<transition>` во Vue, чтобы добиться плавных переходов без лишних усилий. Вместе рассмотрим основные возможности, необходимые CSS-классы и жизненный цикл переходов, а также различные примеры, которые помогут вам сразу интегрировать анимацию в ваши проекты.

## Что такое transition во Vue и зачем он нужен

В библиотеке Vue создание анимированных изменений элементов достигается с помощью специального компонента `<transition>`. Его задача — облегчить добавление CSS анимаций или анимировать изменения на JavaScript при появлении, скрытии или переключении элементов.

Когда вы оборачиваете элемент или компонент в `<transition>`, Vue автоматически добавляет и удаляет определённые CSS-классы на нужных этапах жизненного цикла перехода. Благодаря этому вы можете прописывать стили для разных состояний — и получать плавное, предсказуемое поведение без лишней «магии».

### Когда стоит использовать `<transition>`

- При отображении элементов по условию (v-if, v-show)
- При удалении элементов из DOM
- Для анимации появления вложенных компонентов
- Для простых fade-in/fade-out эффектов
- Для комбинирования анимаций при смене содержимого

Анимация элементов с помощью transition делает интерфейс более привлекательным и интерактивным. Чтобы уверенно работать с transition во Vue, настраивать кастомные классы и оптимизировать производительность, необходимо глубокое понимание Vue.js. Если вы стремитесь освоить плавную анимацию элементов во Vue, рекомендуем наш курс [Vue.js 3, Vue Router и Pinia](https://purpleschool.ru/course/vuejs?utm_source=knowledgebase&utm_medium=article&utm_campaign=ispolzovanie-transition-vo-vue). На курсе 173 урока и 21 упражнение, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Как работает `<transition>` во Vue

Давайте разберёмся, как всё устроено.

### Базовый пример: fade-in и fade-out

Рассмотрим простую задачу — нужно плавно показывать и скрывать элемент на странице:

```html
<template>
  <div>
    <button @click="show = !show">
      Переключить блок
    </button>
    <transition name="fade">
      <p v-if="show">Этот текст появляется и исчезает плавно</p>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: true
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
.fade-enter-to, .fade-leave-from {
  opacity: 1;
}
</style>
```

#### Пояснения к коду

// Кнопка меняет флаг show, управляющий видимостью абзаца
// Элемент `<p>` обернут в `<transition name="fade">`
// CSS-классы отвечают за разные состояния появления и скрытия

#### Под капотом

Когда флаг show переключается:
- Vue добавляет класс `.fade-enter-from` в начале появления элемента и плавно переключает на `.fade-enter-to`.
- При скрытии — добавляет `.fade-leave-from` и затем `.fade-leave-to`.
- Класс `.fade-enter-active` и `.fade-leave-active` управляет самим переходом.

### Управление временем перехода

Вы можете использовать любые свойства CSS transition или animation. Например:

```css
.slide-enter-active, .slide-leave-active {
  transition: all 0.4s cubic-bezier(.55,0,.1,1);
}
.slide-enter-from, .slide-leave-to {
  transform: translateY(-25px);
  opacity: 0;
}
.slide-enter-to, .slide-leave-from {
  transform: translateY(0);
  opacity: 1;
}
```

Теперь элемент будет не только плавно проявляться по прозрачности, но и «прилетать» сверху.

### Применение к v-if и v-show

- `v-if`: элемент добавляется и удаляется из DOM, transition работает при монтировании и размонтировании.
- `v-show`: элемент остается в DOM и управляет только свойством `display`, но transition тоже можно подключить.

**Пример для v-show:**
```html
<transition name="fade">
  <div v-show="visible">Содержимое блока</div>
</transition>
```

Vue обрабатывает анимацию идентично, но имейте в виду: v-show просто переключает display, а v-if действительно добавляет/удаляет элемент из DOM.

### Настройка разных анимаций для появления и исчезновения

Иногда хочется, чтобы появление и исчезновение происходили с разными эффектами. Vue это поддерживает:

```css
.bounce-enter-active {
  animation: bounce-in 0.6s;
}
.bounce-leave-active {
  animation: bounce-out 0.6s;
}
@keyframes bounce-in {
  0%   { transform: scale(0.5); opacity: 0;}
  100% { transform: scale(1); opacity: 1;}
}
@keyframes bounce-out {
  0%   { transform: scale(1); opacity: 1;}
  100% { transform: scale(1.2); opacity: 0;}
}
```

Эффект появления и исчезновения будут разными, при этом компонент остался тем же.

### Пользовательские имена и множественные transition

Вы не ограничены одним вариантом. Можно использовать несколько transition с разными эффектами, просто указывайте соответствующий name.

Также можно динамически менять name:
```html
<transition :name="show ? 'fade' : 'slide'">
  <div v-if="isVisible">Контент</div>
</transition>
```

### Переходы при смене компонентов с помощью `<transition>`

Когда вы используете динамические компоненты (`<component :is="...">`), их также можно анимировать:

```html
<transition name="fade" mode="out-in">
  <component :is="currentComponent"></component>
</transition>
```

**mode="out-in"** гарантирует, что исходный компонент полностью исчезнет, прежде чем появится новый.

### События жизненного цикла transition

Vue позволяет реагировать на этапы transition через события (только для JavaScript-анимаций или дополнительных эффектов):

- `before-enter`
- `enter`
- `after-enter`
- `enter-cancelled`
- `before-leave`
- `leave`
- `after-leave`
- `leave-cancelled`

**Пример использования событий:**

```html
<transition
  @before-enter="beforeEnter"
  @enter="onEnter"
  @after-leave="cleanup"
>
  <div v-if="show">Анимируемый блок</div>
</transition>
```

```js
methods: {
  beforeEnter(el) {
    // Можно задать начальные стили программы
    el.style.opacity = 0
  },
  onEnter(el, done) {
    // Можно использовать сторонние анимационные библиотеки
    $(el).animate({ opacity: 1 }, 500, done)
  },
  cleanup(el) {
    // Что-то убрать, когда анимация закончится
  }
}
```

Эти методы получают доступ к DOM-элементу для ручного управления, если CSS-анимаций недостаточно.

### Безопасная анимация списков через `<transition-group>`

Для анимации добавления, удаления и сортировки элементов в списках используйте `<transition-group>`, который работает с массивами и выводит набор элементов с анимацией:

```html
<template>
  <button @click="addItem">Добавить</button>
  <transition-group name="list" tag="ul">
    <li v-for="item in items" :key="item.id">
      {{ item.text }}
    </li>
  </transition-group>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { id: 1, text: "Первый" },
        { id: 2, text: "Второй" }
      ]
    }
  },
  methods: {
    addItem() {
      this.items.push({ id: Date.now(), text: "Новый" })
    }
  }
}
</script>

<style>
.list-enter-active, .list-leave-active {
  transition: all 0.5s;
}
.list-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
```

#### Особенности

- Используйте уникальный ключ (`:key`) для каждого элемента.
- Можно задавать любой тег для контейнера через `tag`, например, `ul`, `div` или `span`.
- Только тег, указанный в `tag`, будет группировать элементы.

### Управление переходами с помощью JavaScript

Если возможностей CSS недостаточно (например, нужна интеграция с библиотеками анимации), можно полностью контролировать анимацию на JavaScript через методы событий переходит:

```html
<transition
  @enter="customEnter"
  @leave="customLeave"
>
  <div v-if="visible">Кастомная анимация</div>
</transition>
```

```js
methods: {
  customEnter(el, done) {
    // Запуск кастомной анимации появления
    someAnimationLib.show(el, done)
  },
  customLeave(el, done) {
    // Запуск кастомной анимации исчезновения
    someAnimationLib.hide(el, done)
  }
}
```

Главное помнить — вызывайте `done()` для завершения transition.

## Особенности и подводные камни

### Важность уникальных ключей

Для `<transition-group>` всегда указывайте явные и уникальные ключи. Без этого Vue не сможет корректно отслеживать порядок и анимировать перемещения элементов.

### Используйте только один узел внутри `<transition>`

Vue требует, чтобы внутри `<transition>` находился ровно один дочерний элемент. Если нужно передать несколько узлов, используйте обёртку.

### Оптимизация производительности

- Не используйте transition на слишком больших списках или частых изменениях — это может замедлить рендеринг.
- Используйте простые анимации (opacity, transform) — они аппаратно ускоряются и создают минимум нагрузки.

### Совместное использование с animate.css и сторонними библиотеками

Вы легко можете комбинировать transition Vue и внешние библиотеки анимаций, просто добавив нужные классы в события жизненного цикла.

## Заключение

Компонент `<transition>` — это мощный и в то же время простой инструмент для создания плавных анимаций интерфейса на Vue. Он отлично подходит как для простых fade-эффектов, так и для сложных переходов между состояниями компонентов и списков. Используя чётко определённые CSS-классы и события жизненного цикла, вы можете с легкостью кастомизировать поведение анимаций, повысив интерактивность ваших приложений без избыточного кода. Благодаря поддержке работы как с отдельными элементами, так и с группами, transition во Vue остаётся универсальным решением для всех популярных UI-задач.

Для дальнейшего изучения transition во Vue и улучшения навыков работы с анимацией, предлагаем наш курс [Vue.js 3, Vue Router и Pinia](https://purpleschool.ru/course/vuejs?utm_source=knowledgebase&utm_medium=article&utm_campaign=ispolzovanie-transition-vo-vue). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир Vue прямо сегодня.

## Частозадаваемые технические вопросы по теме статьи

### Как указать индивидуальную продолжительность для входа и выхода анимации?

Добавьте дополнительный атрибут `:duration="{ enter: 500, leave: 800 }"` в компонент `<transition>`. Это позволит явно задавать время появления и исчезновения в миллисекундах:
```html
<transition name="fade" :duration="{ enter: 300, leave: 700 }">
  <div v-if="visible"></div>
</transition>
```

### Как анимировать переход между элементами (например, между изображениями)?

Используйте `<transition>` с атрибутом `mode="out-in"`. Это приведёт к тому, что сначала исчезнет текущий элемент, а затем появится новый:
```html
<transition name="fade" mode="out-in">
  <img :src="currentImage" :key="currentImage">
</transition>
```
Убедитесь, что у элементов уникальные ключи.

### Почему transition не работает с v-if, но работает с v-show?

v-if добавляет и удаляет элемент из DOM, если transition не применяется — проверьте структуру HTML (должен быть только один дочерний элемент), наличие необходимых CSS-классов и правильность их имени. Часто забывают задать правильный префикс name.

### Как плавно анимировать изменение свойства (например размер блока), а не появление/исчезновение?

Используйте директиву `<transition>` вокруг блока с v-bind-стилями:
```html
<transition name="resize">
  <div :style="{ width: width + 'px' }" :key="width"></div>
</transition>
```
В CSS для класса `.resize-enter-active, .resize-leave-active` пропишите transition для изменения ширины.

### Можно ли анимировать SVG элементы через transition?

Да, анимация возможна — просто поместите SVG-элемент внутрь `<transition>` и используйте CSS-анимацию для свойств SVG-элемента. Некоторые SVG свойства, такие как transform и opacity, анимируются корректно.
