---
metaTitle: Сигнатуры индекса в TypeScript
metaDescription: Разбираемся как использовать сигнатуры индекса в TypeScript
author: Дмитрий Нечаев
title: Сигнатуры индекса в TypeScript
preview: Учимся пользоваться сигнатурами индекса в TypeScript. Разбираем примеры использования
---

Сигнатуры индекса в TypeScript позволяют динамически определять свойства объектов и массивов, когда полные информации о структуре типов заранее не известны. Этот механизм особенно полезен при работе с данными, структура которых может изменяться в зависимости от условий выполнения программы.

### Основы

Рассмотрим пример, когда вы заранее не знаете имена свойств объекта, но знаете типы значений, которые они могут принимать. В таких случаях можно использовать сигнатуру индекса для описания типов возможных значений. Например, определение интерфейса для массива строк:

```tsx
interface StringArray {
  [index: number]: string;
}

const myArray: StringArray = getStringArray();
const secondItem = myArray[1];  // secondItem имеет тип string

```

В данном примере, интерфейс `StringArray` объявляет, что при обращении по числовому индексу, мы всегда получим строку.

Сигнатуры индекса позволяют определять типы для свойств объектов, ключи которых неизвестны во время компиляции. Чтобы уверенно использовать сигнатуры индекса и создавать надежный код, необходимо глубокое понимание TypeScript. Приходите на наш большой [курс TypeScript с нуля](https://purpleschool.ru/course/typescript?utm_source=knowledgebase&utm_medium=text&utm_campaign=signatury-indeksa-v-typescript). На курсе 192 уроков и 17 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Применение разных типов для индексов

TypeScript поддерживает использование строк или чисел в качестве ключей для сигнатуры индекса. Также возможно использование символов, шаблонных строк или объединений этих типов. Важно понимать, что значения, возвращаемые числовым индексатором, должны быть подтипом значений, возвращаемых строковым индексатором, так как JavaScript преобразует числовые ключи в строки:

```tsx
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

// Ошибка: индексация числом может вернуть другой тип Animal
interface NotOkay {
  [x: number]: Animal;
  [x: string]: Dog;
}

```

### Ограничения и возможности

Индексируемые типы мощный инструмент для работы со словарными структурами данных. Однако они также накладывают ограничения на соответствие типов свойств и значений:

```tsx
interface NumberDictionary {
  [index: string]: number;
  length: number;  // допустимо
  name: string;    // ошибка: тип 'string' не присваиваем типу индекса 'number'
}

```

Однако, если индексируемый тип представляет собой объединение типов, это позволяет содержать свойства разных типов:

```tsx
interface NumberOrStringDictionary {
  [index: string]: number | string;
  length: number;  // допустимо
  name: string;    // допустимо
}

```

### Использование readonly

Для предотвращения изменения значений по индексам, можно использовать модификатор `readonly`:

```tsx
interface ReadonlyStringArray {
  readonly [index: number]: string;
}

let myArray: ReadonlyStringArray = getReadOnlyStringArray();
// Ошибка: изменение значения по индексу запрещено
myArray[2] = "Mallory";

```

### Заключение

Сигнатуры индекса в TypeScript предоставляют гибкость при работе с динамическими структурами данных, позволяя разработчикам определять интерфейсы для объектов и массивов с заранее неизвестными свойствами. Однако важно понимать ограничения, связанные с типами данных и их совместимостью, чтобы эффективно использовать эту возможность языка.

Сигнатуры индекса позволяют создавать более гибкие типы для объектов с динамическими свойствами. На нашем [курсе TypeScript с нуля](https://purpleschool.ru/course/typescript?utm_source=knowledgebase&utm_medium=text&utm_campaign=signatury-indeksa-v-typescript) вы получите необходимые знания и практические навыки. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в TypeScript прямо сегодня.
