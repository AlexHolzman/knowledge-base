---
metaTitle: Как отключить определенные функции в Nuxt
metaDescription: Освойте способы отключения отдельных функций в Nuxt - будь то плагины, middleware, auto import или другие возможности, и настройте фреймворк под свои задачи
author: Олег Марков
title: Как отключить определенные функции в Nuxt
preview: Пошаговая инструкция по отключению функционала в Nuxt — легко управляйте автоимпортами, мидлвеарами, плагинами, роутингом и другими функциями проекта
---

## Введение

Nuxt — это мощный фреймворк на базе Vue, который автоматизирует множество аспектов разработки фронтенда и SSR-приложений. Однако не всегда стандартные возможности Nuxt нужны во всех проектах. Иногда возникает задача отключить определённые фичи: например, автоматический импорт компонентов, плагины, middleware, роутинг, или специфические модули.

В этой статье я расскажу, как выборочно выключить такие функции в Nuxt 2 и Nuxt 3. Мы разберём как временно “приглушить” какое-то поведение во время разработки, так и полностью убрать неиспользуемый функционал из production-сборки. Вы увидите, как деактивировать автоматический импорт компонентов, отключать middleware, убирать плагины, перестраивать роутинг под себя и отключать отдельные модули. Всё это будет показано на примерах из реальных проектов Nuxt.

## Отключение автоматического импорта компонентов

В Nuxt 2 и Nuxt 3 автоматический импорт компонентов делает процесс разработки значительно проще: любой компонент из папки `components` становится доступен в шаблонах без необходимости явного импорта. Но если вам нужна строгая изоляция, контроль или оптимизация, можно отключить этот механизм.

### Отключение в Nuxt 2

В Nuxt 2 этот функционал реализован через опцию `components` в `nuxt.config.js`. По умолчанию она равна `false`, но многие шаблоны или плагины могут включать её. Пример:

```js
// nuxt.config.js
export default {
  components: false // Отключаем автоматическую регистрацию компонентов
}
```
После этого вам придётся явно импортировать и регистрировать компоненты в каждом файле Vue:

```js
<script>
import MyButton from '~/components/MyButton.vue'

export default {
  components: {
    MyButton // Явная регистрация
  }
}
</script>
```
### Отключение в Nuxt 3

В Nuxt 3 отключение автоимпорта делается аналогично:

```js
// nuxt.config.ts
export default defineNuxtConfig({
  components: false // Полное отключение
})
```
Если хочется отключить импорт только некоторых директорий, можно использовать массив или передать более сложную конфигурацию, например:

```js
export default defineNuxtConfig({
  components: [
    { path: '~/components', pathPrefix: false, enabled: false }, // Только конкретная папка
  ]
})
```

Отключение определенных функций может быть необходимо для оптимизации Nuxt-приложений или для решения проблем совместимости. Чтобы делать это безопасно и эффективно, нужно понимать, как работает конфигурация Nuxt, какие функции можно отключать и какие последствия это может иметь. Если вы хотите научиться отключать определенные функции в Nuxt, приходите на наш большой курс [Nuxt - fullstack Vue фреймворк](https://purpleschool.ru/course/nuxt?utm_source=knowledgebase&utm_medium=article&utm_campaign=kak-otklyuchit-opredelennye-funktsii-v-nuxt). На курсе 129 уроков и 13 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Особенности ручного импорта

Отключив автоимпорт, стоит помнить, что:

- Вам нужно всегда явно импортировать компоненты.
- Неиспользуемые компоненты не попадут в сборку.
- Вы сможете точнее контролировать “разрастание” клиентского кода (bundle).

## Отключение или настройка middleware

Middleware — это код, который запускается до того, как страница будет отрисована или роут обработан. В некоторых случаях вы захотите их временно отключить (например, для отладки) или полностью убрать определённое поведение.

### Отключение middleware в Nuxt 2

В Nuxt 2 middleware регистрируются либо глобально через `nuxt.config.js`:

```js
export default {
  router: {
    middleware: ['auth']
  }
}
```

Чтобы убрать глобальное middleware, удалите или закомментируйте свойство:

```js
export default {
  router: {
    // middleware: ['auth']
  }
}
```

Если middleware используется только на уровне страниц, удалите соответствующее свойство из компонентов страниц:

```js
export default {
  // middleware: 'auth'
}
```
### Отключение middleware в Nuxt 3

В Nuxt 3 структура middleware стала более унифицированной — файлы лежат в папке `middleware`. Автоматическое подключение происходит только если вы явно указываете middleware на странице или в роуте.

Удалите вызов middleware из вашего файла страницы:

```js
definePageMeta({
  // middleware: 'auth'
})
```

Или переименуйте/удалите сам файл middleware, чтобы он не был доступен.

## Управление и отключение плагинов

Плагины в Nuxt подключаются для расширения функционала приложения (например, глобальный импорт библиотек, настроек, фильтров и т.д).

### Отключение плагинов в Nuxt 2

Плагины регистрируются через массив `plugins` в `nuxt.config.js`:

```js
export default {
  plugins: [
    '~/plugins/my-plugin.js'
  ]
}
```

Чтобы отключить плагин, просто закомментируйте или удалите его из списка:

```js
export default {
  plugins: [
    // '~/plugins/my-plugin.js'
  ]
}
```

### Отключение плагинов в Nuxt 3

В Nuxt 3 все плагины, размещенные в папке `/plugins`, автоматически подключаются. Если нужно временно отключить плагин, просто переименуйте его файл — например, с `my-plugin.ts` на `_my-plugin.ts`, или переместите его в другую директорию:

```
// plugins/_my-plugin.ts
// Переименованный плагин не будет зарегистрирован в проекте
```

Если нужно динамически контролировать подключение, вы также можете использовать условия внутри файлов конфига или самих плагинов, проверяя переменные окружения.

## Отключение модулей

Модули (Modules) позволяют расширять возможности Nuxt — подгружать сторонние библиотеки, интеграцию с API и т.п. Управляются через секцию `modules` в конфиге.

```js
export default {
  modules: [
    '@nuxtjs/axios',
    'nuxt-i18n'
  ]
}
```

Если вам не нужно какое-то расширение, просто удалите его из массива `modules` либо закомментируйте:

```js
export default {
  modules: [
    // '@nuxtjs/axios'
  ]
}
```

Также не забудьте удалить любые связанные настройки из других секций, если они есть — это поможет избежать ошибок при запуске.

## Настройка роутинга и отключение авто-генерации маршрутов

Автоматическая генерация маршрутов — одна из “фишек” Nuxt: структура каталогов `pages` определяет структуру роутов. Иногда это не нужно, например, если вы хотите использовать custom router или динамически формировать роуты на основе особых условий.

### Отключение auto-routing в Nuxt 2

В Nuxt 2 вы можете добавить свойство `router` с полем `extendRoutes` в конфигурацию:

```js
// nuxt.config.js
export default {
  router: {
    extendRoutes(routes, resolve) {
      // Полностью очищаем стандартные роуты
      routes.splice(0)
      routes.push({
        name: 'custom',
        path: '/custom',
        component: resolve(__dirname, 'pages/custom.vue')
      })
    }
  }
}
```

Таким образом, стандартная генерация роутинга на базе файлов из `pages` больше не будет использоваться.

### Отключение auto-routing в Nuxt 3

В Nuxt 3 возможности полный отказ от файловой структуры роутов стандартно не предусмотрен: роутинг строится из файлов в `pages`. Но вы можете создавать “пустую” папку `pages`, размещая кастомные файлы роутера в модулях, либо использовать сторонние пакеты для собственного роутинга.

Для продвинутого управления, создайте модуль, который реализует custom router, либо организуйте папку `pages` так, чтобы там были только те маршруты, которые вам нужны.

## Отключение автоимпорта composables и utils

В Nuxt 3 появилась возможность автоматического импорта composables (реактивных методов, хуков), которые лежат в папке `composables`.

Если вы хотите отключить этот функционал:

```js
// nuxt.config.ts
export default defineNuxtConfig({
  imports: {
    dirs: []
  }
})
```
Такой подход полностью отключит автоимпорт из всех стандартных папок.

Также можно поиграть с конфигурацией, чтобы отключить только часть директорий или кастомизировать путь:

```js
export default defineNuxtConfig({
  imports: {
    dirs: [
      // Оставьте только те папки, которые нужны
      // 'composables', 'utils' и т.д., иначе оставьте массив пустым
    ]
  }
})
```

## Управление и отключение серверного рендера (SSR)

Иногда требуется полностью отключить SSR — например, если вы планируете проводить полный рендеринг только на клиенте.

### Отключение SSR в Nuxt 2

```js
export default {
  ssr: false // Сборка только client-side
}
```

### Отключение SSR в Nuxt 3

```js
export default defineNuxtConfig({
  ssr: false // Только клиентский рендеринг
})
```

После этого Nuxt перестанет рендерить страницы на сервере.

## Деактивация специфических функций через переменные окружения

Иногда удобно не полностью убирать код, а “отключать” логикой переменных окружения:

```js
// nuxt.config.ts
export default defineNuxtConfig({
  components: process.env.NUXT_COMPONENTS === 'true'
})
```

Внутри плагинов, middleware, composables или любых других функций вы можете выполнять проверку через `process.env`, чтобы рантайм-контроль был максимально гибким.

## Отключение PWA, Telemetry и других “скрытых” функций

### Отключение поддержки PWA

Если вы использовали модуль `@nuxtjs/pwa`, удалите его из раздела `modules`, а сами файлы сервис-воркера из папки `static` или `public`.

### Отключение Telemetry

Nuxt c определённой версии “собирает” анонимную телеметрию, чтобы улучшить продукт. Чтобы отключить её, пропишите в проекте (однократно):

```
npx nuxi telemetry disable
```
или для Nuxt 2:

```
npx nuxt telemetry disable
```

Аналогично работает и переменная окружения:

```
NUXT_TELEMETRY_DISABLED=1
```

## Отключение глобальных стилей и head метатегов

Файлы глобальных стилей подключаются через секции `css` и `head`. Чтобы убрать их:

```js
export default {
  css: [
    // 'assets/main.css'
  ],
  head: {
    meta: [
      // { name: 'description', content: 'Website Description' }
    ]
  }
}
```
И удаляйте из используемой темы или layout те импорты, которые вам не нужны.

## Использование кастомной сборки

Если задача — не только “выключить” фичу, но и убрать из финального бандла, рекомендуют:

- Отключать фичи на уровне конфига;
- Переименовывать файлы, чтобы Nuxt не “видел” их автоматически;
- Динамически строить список плагинов/модулей по переменным окружения;
- Проверять свои импорты, чтобы не тащить неиспользуемый код.

## Заключение

Проекты на Nuxt часто требуют тонкой подстройки: иногда автоимпорт компонентов работает в плюс, иногда мешает поддерживать строгую архитектуру. Плагины могут быть полезны на dev-стадии, но не нужны в продукте. Middleware должны быть гибко управляемыми, роутинг — легко переопределяемым.

Nuxt позволяет отключить практически любую автоматизацию или функцию. Это достигается либо прямыми настройками в конфиге, либо через удаление файлов из нужных директорий, либо управлением через переменные окружения. Используйте эти подходы для тонкой настройки производительности, безопасности и удобства поддержки ваших проектов.

Возможность отключать определенные функции - это лишь один из способов кастомизации Nuxt-приложений. Чтобы создавать гибкие и масштабируемые приложения, необходимо освоить все возможности фреймворка, включая работу с сервером, базами данных и API. На нашем курсе [Nuxt - fullstack Vue фреймворк](https://purpleschool.ru/course/nuxt?utm_source=knowledgebase&utm_medium=article&utm_campaign=kak-otklyuchit-opredelennye-funktsii-v-nuxt) вы найдете все необходимые знания и навыки для достижения успеха. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в Nuxt прямо сегодня.

## Частозадаваемые технические вопросы по теме статьи и ответы на них

### Как отключить SSR только для определённых страниц в Nuxt 3?

Nuxt 3 не поддерживает выборочное отключение SSR на уровне отдельных страниц из коробки. Если вам нужно клиентское поведение для части приложения — используйте динамические импорты с `mode: 'client'` или подход `onMounted`/`client-only` компонент на страницах для изоляции клиентского функционала.

### Как отключить автоматический импорт store или Vuex в Nuxt 2?

До появления нового `useState`, модуль store/Vuex подключается автоматически, если есть папка `store`. Чтобы отключить store, просто переименуйте либо удалите папку `store` из корня проекта. Тогда Nuxt больше не будет инициализировать Vuex.

### Можно ли отключить только часть middleware, но не всю папку?

Да, просто удалите или переименуйте конкретные файлы middleware, которые не хотите использовать. Если middleware подключено явно в настройках страниц или роутера, уберите соответствующее свойство `middleware` на нужных страницах.

### Как программно управлять плагинами на основе окружения?

В конфигах (nuxt.config.js/nuxt.config.ts) можете формировать массив `plugins` или `modules` динамически:

```js
plugins: process.env.FEATURE_ENABLED ? ['~/plugins/feature.js'] : []
```
Это позволит включать и отключать плагины в зависимости от среды разработки или сборки.

### Почему после отключения auto-import/components возникают ошибки о не найденных компонентах?

Система auto-import больше не регистрирует компоненты глобально. Чтобы это исправить — для каждого используемого компонента выполните явный импорт и регистрацию в секции `components` внутри соответствующих компонентов Vue или используйте локальные импорты.
