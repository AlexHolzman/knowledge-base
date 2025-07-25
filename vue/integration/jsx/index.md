---
metaTitle: Примеры использования JSX во Vue
metaDescription: Изучите реальные примеры применения JSX во Vue - посмотрите, как использовать альтернативный синтаксис для создания компонентов с гибкостью React, узнавайте о настройке, особенностях и преимуществах подхода
author: Олег Марков
title: Примеры использования JSX во Vue
preview: Погрузитесь в примеры и преимущества использования JSX во Vue - настройка, базовый синтаксис, генерация списков, работа с обработчиками и доступ к атрибутам, рекомендации из практики
---

## Введение

Vue традиционно ассоциируется с использованием шаблонов (`template`), которые легко читаются даже теми, кто только начинает работать с этим фреймворком. Однако не все знают, что Vue прекрасно работает и с JSX – синтаксисом, популярным среди разработчиков React. JSX позволяет писать разметку непосредственно внутри JavaScript, даёт мощную динамику, улучшает возможности композиции, да и просто нравится многим разработчикам, привыкшим к таким шаблонам.

В этой статье я покажу, как на практике использовать JSX во Vue – вы увидите, как это настраивается, какие подходы к организации кода доступны и какие задачи проще решать именно через JSX. Уверен, что после нескольких примеров вы без труда сможете применять эту технологию в своих проектах.

Использование JSX во Vue открывает новые возможности для создания компонентов с гибкостью React. Если вы хотите освоить альтернативный синтаксис для создания компонентов и понять преимущества JSX, то наш курс [Vue.js 3, Vue Router и Pinia](https://purpleschool.ru/course/vuejs?utm_source=knowledgebase&utm_medium=article&utm_campaign=primery-ispolzovaniya-jsx-vo-vue) будет для вас отличным выбором. На курсе 173 урока и 21 упражнение, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами. Вы получите глубокие знания по основам Vue.js, работе с компонентами, шаблонами и многим другим аспектам.

## Настройка поддержки JSX во Vue

### Как подключить поддержку JSX

По умолчанию во Vue (особенно в версиях Vue 2 и 3) нужно явно добавить поддержку JSX через плагины для сборщиков типа Vite или Webpack.

#### Для Vue 3 с Vite

1. Установите нужный плагин:

```
npm install @vitejs/plugin-vue-jsx --save-dev
```

2. Подключите плагин в `vite.config.js`:

```js
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';
import vueJsx from '@vitejs/plugin-vue-jsx';

export default defineConfig({
  plugins: [vue(), vueJsx()], // Подключаем оба плагина
});
```
  
#### Для Vue 3 с Webpack

Используйте Babel плагин для JSX:

```
npm install @vue/babel-plugin-jsx --save-dev
```

И добавьте его в настройки Babel (например, в `babel.config.js`):

```js
module.exports = {
  plugins: ['@vue/babel-plugin-jsx'],
};
```

### Применение в SFC (Single File Components)

Вместо секции `<template>` используйте `<script lang="jsx">` или просто `.jsx` или `.tsx` файл:

```js
// Пример MyComponent.jsx
import { defineComponent } from 'vue';

export default defineComponent({
  setup() {
    return () => <div>Привет из JSX!</div>;
  }
});
```

Обратите внимание: весь рендеринг теперь происходит через функцию `setup`, которая возвращает функцию рендера.

## Базовый синтаксис JSX во Vue

### Как объявлять элементы

JSX позволяет объявлять структуру компонентов прямо внутри JS:

```js
return () => <h1>Заголовок через JSX</h1>;
```

Можно вкладывать элементы:

```js
return () => (
  <section>
    <h1>Внутри секции</h1>
    <p>Описание компонента</p>
  </section>
);
```

Для динамических атрибутов используйте фигурные скобки:

```js
const title = "Это динамический заголовок";
return () => <h1>{title}</h1>;
```

### Использование условных операторов и циклов

В JSX часто применяют тернарный оператор и map:

```js
const show = true;
return () => (
  <div>
    {show ? <span>Видно</span> : <span>Скрыто</span>}
  </div>
);
```

Генерация списка на основе массива:

```js
const items = ['яблоко', 'банан', 'апельсин'];
return () => (
  <ul>
    {items.map((fruit, i) => (
      <li key={i}>{fruit}</li>
    ))}
  </ul>
);
```
  
## Передача и обработка props, событий и слотов

### Передача props

В JSX props передаются как атрибуты элемента:

```js
const MyButton = (props) => <button>{props.label}</button>;

// Использование
<MyButton label="Нажми меня" />
```

### Обработка событий

События работают почти так же, как в React или обычном Vue, только именование событий — в верблюжьем стиле:

```js
<button onClick={() => alert("Клик по кнопке!")}>Кликни!</button>
```

Если вы передаёте функцию, не забывайте про стрелочные функции или bind.

### Использование слотов

Иногда в JSX их называют "children". Пример простой передачи слота:

```js
const Panel = (props, { slots }) => (
  <div class="panel">
    {slots.default ? slots.default() : null}
  </div>
);
// Использование
<Panel>
  <p>Контент панели</p>
</Panel>
```

В Vue 3 c Composition API доступ к слотам осуществляется через второй аргумент setup-функции.

### Передача и обработка ref

Для работы с ref используйте директиву ref напрямую:

```js
import { ref } from 'vue';

export default defineComponent({
  setup() {
    const inputRef = ref(null);
    const focusInput = () => {
      inputRef.value && inputRef.value.focus();
    };

    // input связывается с ref
    return () => (
      <>
        <input ref={inputRef} />
        <button onClick={focusInput}>Фокус</button>
      </>
    );
  }
});
```

## Расширенные примеры работы с JSX

### Создание динамических компонентов

Смотрите, как можно выбирать компонент для рендеринга на лету:

```js
const DynamicComponent = defineComponent({
  props: {
    type: String // Например, 'input' или 'select'
  },
  setup(props) {
    return () =>
      props.type === 'input'
        ? <input placeholder="Введите текст"/>
        : <select>
            <option>Выберите</option>
          </select>
  }
});
// Использование
<DynamicComponent type="input" />
```

### Обработка событий с передачей параметров

Если нужно передать параметры в обработчик события:

```js
<button onClick={() => handleClick(item.id)}>Удалить</button>
```

Или использовать bind:

```js
<button onClick={handleClick.bind(null, item.id)}>Удалить</button>
```

### Использование директив v-model в JSX

В Vue 3 появилась поддержка двухсторонней привязки через `v-model`:

```js
import { ref } from 'vue';

export default defineComponent({
  setup() {
    const name = ref('');
    return () => (
      <input v-model={name.value} />
    );
  }
});
```

Однако по факту, в чисто JSX-компонентах v-model заменяется на пару props+event:

```js
<input value={name.value} onInput={e => name.value = e.target.value} />
```

### Кастомные директивы (аналог v-if / v-for)

Вместо v-if — используйте обычные условия:

```js
{visible && <div>Покажи меня!</div>}
```

Вместо v-for — map, как выше.

#### Пример с динамическими стилями и классами

```js
const isActive = true;
const styles = { color: 'red', fontWeight: 'bold' };
return () => (
  <div class={{ active: isActive, disabled: !isActive }} style={styles}>
    Динамические классы и стили
  </div>
);
```

Обратите внимание: для классов используйте объект — ключи будут классами, значения — булевы выражения.

## Когда выбирать JSX во Vue

### Преимущества

- **Гибкость**: вся сила JavaScript под рукой, нет ограничений шаблона.
- **Переиспользуемость взаимных блоков разметки**: проще строить функции, возвращающие разметку.
- **Динамическая генерация компонентов, вложенные функции**: удобно организовывать сложные структуры.

### Недостатки

- Чуть меньше декларативности и простоты для новичков.
- Шаблоны проще читаются при верстке.
- Нужно дополнительное подключение плагинов.

## Хорошие сценарии для применения JSX

- Когда компонент действительно сложный и требует много вычисляемой, условно-динамической разметки.
- Если ваша команда знакома с React и привыкла к схожей организации кода.
- При необходимости написать множество вспомогательных функций для генерации блоков или часто менять обработчики событий.

## Заключение

JSX становится все более уместным выбором в мире Vue для решения задач, когда простые шаблоны уже не справляются с динамикой или требуют слишком сложных вычислений. Вы узнали, как настроить поддержку JSX, как выглядит базовый и расширенный синтаксис, как реализуются типовые и нестандартные шаблонные сценарии с помощью JSX. Свободное сочетание Vue и JSX позволяет вам оставаться продуктивным и реализовывать самые амбициозные задумки.

Чтобы закрепить знания о JSX и углубить понимание Vue.js, пройдите наш курс [Vue.js 3, Vue Router и Pinia](https://purpleschool.ru/course/vuejs?utm_source=knowledgebase&utm_medium=article&utm_campaign=primery-ispolzovaniya-jsx-vo-vue). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир Vue прямо сегодня.

## Частозадаваемые технические вопросы по теме

### Как подключить глобальные расширения (например, плагины), если я пишу компоненты только на JSX?

Если вы используете только JSX-компоненты, используйте функцию `app.use(plugin)` в вашем основном файле (обычно `main.js`). Это не зависит от синтаксиса компонентов – плагины будут доступны во всей иерархии компонентов, включая те, что на JSX.

### Почему мои props не типизируются в JSX, как это делается в типовом Vue SFC?

В JSX можно использовать TypeScript для типизации props: объявите их в defineComponent, а для функциональных компонентов используйте Generic-параметры. Пример:

```js
const MyComponent: FunctionalComponent<{ count: number }> = (props) => <span>{props.count}</span>;
```

### Почему не работают шаблонные директивы (например, v-if, v-for, v-show) в JSX?

JSX-интерпретация не поддерживает директивы прямо — используйте JavaScript-условия, тернарные операторы, циклы map и собственные условия для контролирования вывода.

### Как правильно подключать scoped-стили в компонентах на JSX?

Scoped-стили работают на уровне `<style scoped>` в SFC. Для JSX компонентов используйте CSS-модули, библиотеку CSS-in-JS или глобальные классы. Например, с Vite можно импортировать CSS-модуль и применять классы через объект.

### Можно ли использовать JSX в миксинах или директивах?

Да, вы можете описывать render-функции в миксинах или создавать пользовательские директивы для Vue, возвращающие JSX-элементы, если ваш сборщик поддерживает JSX. Подключение ничем не отличается от обычных компонентов.
