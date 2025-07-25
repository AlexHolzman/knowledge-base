---
metaTitle: window.open() – JavaScript Browser Environment And API – Браузерное окружение и API в JS
metaDescription: Как работает window.open() в JS | База знаний PurpleSchool
author: Дмитрий Фандорин
title: window.open() в JavaScript
preview: window.open() - это функция в JavaScript, которая используется для открытия нового окна браузера с заданными параметрами...
---

window.open() - это функция в JavaScript, которая используется для открытия нового окна браузера с заданными параметрами.

Пример использования функции window.open() для открытия нового окна:

```javascript
window.open('https://www.example.com', '_blank');
```

В этом примере вызывается функция window.open() с двумя аргументами: URL-адресом и именем окна. Эта функция открывает новое окно браузера и загружает в нем указанный URL-адрес.

## Форма записи

Функция window.open() вызывается с тремя или четырьмя аргументами. Форма записи функции window.open() выглядит следующим образом:

```javascript
window.open(url, name, features, replace);
```

- url: URL-адрес страницы, которую нужно открыть в новом окне. Этот аргумент является обязательным.
- name: Имя, которое будет присвоено новому окну. Этот аргумент может быть пустым или принимать одно из следующих значений:
  - "_blank": открыть ссылку в новом окне.
  - "_self": загрузить ссылку в текущем окне.
  - "_parent": загрузить ссылку в родительском фрейме.
  - "_top": загрузить ссылку в верхнем фрейме.
  - Имя существующего окна: загрузить ссылку в указанном окне.
- features: Список параметров, которые определяют поведение нового окна. Этот аргумент может быть пустым или содержать один или несколько параметров, разделенных запятыми.
- replace: Определяет, следует ли заменить текущую страницу новой страницей. Этот аргумент может принимать два значения: true или false.

Пример:

```javascript
window.open('https://www.example.com', '_blank', 'width=500,height=500,resizable=yes');
```

В этом примере открывается новое окно с URL-адресом "https://www.example.com", именем "_blank" и параметрами ширины, высоты и возможности изменения размера окна.

## Заключение

Функция window.open() - это мощный инструмент для открытия новых окон браузера с помощью JavaScript. Она позволяет определять размеры, положение и поведение нового окна и может быть использована для создания всплывающих окон и открытия веб-страниц в новых окнах. Однако ее использование может быть заблокировано некоторыми браузерами в целях безопасности, поэтому ее следует использовать с осторожностью.

Работа с окнами браузера - важная часть веб-разработки, но для создания современных веб-приложений вам потребуются более глубокие знания. Мы приглашаем вас на наш продвинутый курс **[JavaScript Advanced](https://purpleschool.ru/course/javascript-advanced?utm_source=knowledgebase&utm_medium=text&utm_campaign=window-open-v-javascript)**, где вы сможете изучить асинхронное программирование, принципы ООП и другие важные концепции. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир JavaScript прямо сегодня.
