---
metaTitle: Псевдокласс placeholder-shown в CSSю Стилизация полей с плейсхолдером
metaDescription: Псевдокласс placeholder-shown в CSS. Стилизация полей с плейсхолдером
author: Дмитрий Нечаев
title: Псевдокласс placeholder-shown в CSS. Полное руководство с примерами
preview: Псевдокласс placeholder-shown в CSS используется для стилизации полей ввода, в которых отображается плейсхолдер.
---

Псевдокласс `:placeholder-shown` в CSS используется для стилизации полей ввода, в которых отображается плейсхолдер. Это позволяет разработчикам изменять внешний вид полей формы, когда в них ничего не введено, предоставляя визуальные подсказки для пользователей. В этой статье мы подробно рассмотрим псевдокласс `:placeholder-shown`, его применение и приведём примеры использования для различных ситуаций.

## Что такое псевдокласс `:placeholder-shown`?

Псевдокласс `:placeholder-shown` применяется к полям формы, в которых отображается плейсхолдер. Этот псевдокласс позволяет стилизовать поля ввода до тех пор, пока пользователь не начал вводить текст.

Работа с плейсхолдерами подразумевает не только стилизацию, но и понимание структуры HTML-форм и способов взаимодействия с пользовательским вводом. Без знания основ HTML и CSS даже самый элегантный псевдокласс `placeholder-shown` окажется бесполезным. Если вы хотите детальнее разобраться в принципах создания веб-форм и их стилизации — приходите на наш большой курс [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=Psevdoklass-placeholder-shown-v-CSS-Polnoe-rukovodstvo-s-primerami). На курсе 212 уроков и 19 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Пример базового использования `:placeholder-shown`

```css
input:placeholder-shown {
  /* Стили для полей ввода с отображаемым плейсхолдером */
}

```

Пример использования псевдокласса `:placeholder-shown` для изменения стилей полей ввода с плейсхолдером:

```css
input:placeholder-shown {
  border-color: gray;
}

```

В этом примере поля ввода с плейсхолдером будут иметь серую границу.

## Примеры использования псевдокласса `:placeholder-shown`

### Основные примеры

### Стилизация текстовых полей

Пример:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    input:placeholder-shown {
      border: 2px solid gray; /* Серая граница для полей ввода с плейсхолдером */
      background-color: #f0f0f0; /* Светло-серый фон */
    }
  </style>
  <title>Стилизация текстовых полей</title>
</head>
<body>
  <form>
    <label for="name">Имя:</label>
    <input type="text" id="name" name="name" placeholder="Введите ваше имя">
    <br>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" placeholder="Введите ваш email">
  </form>
</body>
</html>

```

В этом примере поля ввода с плейсхолдером будут иметь серую границу и светло-серый фон.

### Стилизация текстовых областей

Пример:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    textarea:placeholder-shown {
      border: 2px solid gray; /* Серая граница для текстовых областей с плейсхолдером */
      background-color: #f0f0f0; /* Светло-серый фон */
    }
  </style>
  <title>Стилизация текстовых областей</title>
</head>
<body>
  <form>
    <label for="message">Сообщение:</label>
    <textarea id="message" name="message" placeholder="Введите ваше сообщение"></textarea>
  </form>
</body>
</html>

```

В этом примере текстовая область с плейсхолдером будет иметь серую границу и светло-серый фон.

### Сложные примеры

### Стилизация с использованием псевдоэлементов

Пример:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    .form-field {
      position: relative;
      margin-bottom: 20px; /* Отступ снизу для каждого поля формы */
    }

    input:placeholder-shown,
    textarea:placeholder-shown {
      border: 2px solid gray; /* Серая граница для полей с плейсхолдером */
      background-color: #f0f0f0; /* Светло-серый фон */
      padding-right: 30px; /* Внутренний отступ справа для иконки */
    }

    input:placeholder-shown:before,
    textarea:placeholder-shown:before {
      content: "🔍"; /* Иконка лупы для поиска */
      position: absolute;
      right: 10px;
      top: 50%;
      transform: translateY(-50%);
      color: gray;
      font-size: 20px;
    }
  </style>
  <title>Стилизация с использованием псевдоэлементов</title>
</head>
<body>
  <form>
    <div class="form-field">
      <label for="search">Поиск:</label>
      <input type="text" id="search" name="search" placeholder="Введите запрос">
    </div>
    <button type="submit">Найти</button>
  </form>
</body>
</html>

```

В этом примере к полям ввода добавлена иконка лупы, используя псевдоэлемент `:before`, если отображается плейсхолдер.

### Комбинирование с другими псевдоклассами

Пример:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    input:placeholder-shown:focus,
    textarea:placeholder-shown:focus {
      border-color: blue; /* Синяя граница при фокусе */
      box-shadow: 0 0 5px blue; /* Тень синего цвета */
    }
  </style>
  <title>Комбинирование с другими псевдоклассами</title>
</head>
<body>
  <form>
    <label for="username">Имя пользователя:</label>
    <input type="text" id="username" name="username" placeholder="Введите имя пользователя">
  </form>
</body>
</html>

```

В этом примере граница и тень поля ввода изменяются при фокусе, если отображается плейсхолдер.

## Использование в реальных проектах

### Стилизация формы регистрации

Пример использования псевдокласса `:placeholder-shown` для стилизации полей в форме регистрации:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    form {
      max-width: 400px;
      margin: 20px auto;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 5px;
      background-color: #f9f9f9;
    }

    .form-field {
      margin-bottom: 15px; /* Отступ снизу для каждого поля формы */
    }

    .form-field label {
      display: block; /* Блочное отображение */
      margin-bottom: 5px; /* Отступ снизу */
    }

    .form-field input,
    .form-field textarea {
      width: 100%; /* Ширина 100% */
      padding: 8px; /* Внутренние отступы */
      box-sizing: border-box; /* Учет границы в ширину */
    }

    input:placeholder-shown,
    textarea:placeholder-shown {
      border: 2px solid gray; /* Серая граница для полей с плейсхолдером */
      background-color: #f0f0f0; /* Светло-серый фон */
    }

    .submit-button {
      background-color: #007bff; /* Фон кнопки */
      color: white; /* Цвет текста */
      padding: 10px 20px; /* Внутренние отступы */
      border: none; /* Без границы */
      border-radius: 5px; /* Скругление углов */
      cursor: pointer; /* Курсор указателя */
      display: block; /* Блочное отображение */
      width: 100%; /* Ширина 100% */
      box-sizing: border-box; /* Учет границы в ширину */
    }

    .submit-button:hover {
      background-color: #0056b3; /* Изменение фона при наведении */
    }
  </style>
  <title>Стилизация формы регистрации</title>
</head>
<body>
  <form>
    <div class="form-field">
      <label for="name">Имя:</label>
      <input type="text" id="name" name="name" placeholder="Введите ваше имя">
    </div>
    <div class="form-field">
      <label for="email">Email:</label>
      <input type="email" id="email" name="email" placeholder="Введите ваш email">
    </div>
    <div class="form-field">
      <label for="password">Пароль:</label>
      <input type="

password" id="password" name="password" placeholder="Введите пароль">
    </div>
    <div class="form-field">
      <label for="bio">О себе:</label>
      <textarea id="bio" name="bio" placeholder="Расскажите о себе"></textarea>
    </div>
    <button type="submit" class="submit-button">Регистрация</button>
  </form>
</body>
</html>

```

В этом примере все поля ввода и текстовая область с плейсхолдером в форме регистрации будут стилизованы с серой границей и светло-серым фоном.

### Стилизация формы обратной связи

Пример использования псевдокласса `:placeholder-shown` для стилизации полей в форме обратной связи:

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    form {
      max-width: 500px;
      margin: 20px auto;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 5px;
      background-color: #f9f9f9;
    }

    .form-field {
      margin-bottom: 20px; /* Отступ снизу для каждого поля формы */
    }

    .form-field label {
      display: block; /* Блочное отображение */
      margin-bottom: 5px; /* Отступ снизу */
    }

    .form-field input,
    .form-field textarea {
      width: 100%; /* Ширина 100% */
      padding: 10px; /* Внутренние отступы */
      box-sizing: border-box; /* Учет границы в ширину */
    }

    input:placeholder-shown,
    textarea:placeholder-shown {
      border: 2px solid gray; /* Серая граница для полей с плейсхолдером */
      background-color: #f0f0f0; /* Светло-серый фон */
    }

    .submit-button {
      background-color: #28a745; /* Фон кнопки */
      color: white; /* Цвет текста */
      padding: 10px 20px; /* Внутренние отступы */
      border: none; /* Без границы */
      border-radius: 5px; /* Скругление углов */
      cursor: pointer; /* Курсор указателя */
      display: block; /* Блочное отображение */
      width: 100%; /* Ширина 100% */
      box-sizing: border-box; /* Учет границы в ширину */
    }

    .submit-button:hover {
      background-color: #218838; /* Изменение фона при наведении */
    }
  </style>
  <title>Стилизация формы обратной связи</title>
</head>
<body>
  <form>
    <div class="form-field">
      <label for="name">Имя:</label>
      <input type="text" id="name" name="name" placeholder="Введите ваше имя">
    </div>
    <div class="form-field">
      <label for="email">Email:</label>
      <input type="email" id="email" name="email" placeholder="Введите ваш email">
    </div>
    <div class="form-field">
      <label for="message">Сообщение:</label>
      <textarea id="message" name="message" rows="5" placeholder="Введите ваше сообщение"></textarea>
    </div>
    <button type="submit" class="submit-button">Отправить</button>
  </form>
</body>
</html>

```

В этом примере все поля ввода и текстовая область с плейсхолдером в форме обратной связи будут стилизованы с серой границей и светло-серым фоном.

## Заключение

Псевдокласс `:placeholder-shown` в CSS предоставляет удобный способ для стилизации полей формы, в которых отображается плейсхолдер. Это помогает улучшить пользовательский интерфейс, предоставляя визуальные подсказки и делая форму более интуитивно понятной. Понимание различных способов использования псевдокласса `:placeholder-shown`, а также его комбинирование с другими селекторами и псевдоклассами, помогает разработчикам создавать более гибкие и адаптивные стили. Экспериментируйте с различными подходами и находите оптимальные решения для ваших проектов.

Псевдокласс `:placeholder-shown` позволяет создавать более информативные и удобные формы. Чтобы освоить этот и другие инструменты веб-разработки, необходима прочная база знаний. Курс [HTML и CSS](https://purpleschool.ru/course/html-css?utm_source=knowledgebase&utm_medium=text&utm_campaign=Psevdoklass-placeholder-shown-v-CSS-Polnoe-rukovodstvo-s-primerami) предоставит вам необходимые знания и навыки для создания современных и привлекательных веб-интерфейсов. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир HTML и CSS прямо сегодня.
