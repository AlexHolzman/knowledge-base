---
metaTitle: Float в Golang
metaDescription: Изучаем работу с типом данных float в языке программирования Go (Golang).
author: Дмитрий Нечаев
title: Float в Golang
preview: В этой статье мы рассмотрим, что представляет собой тип данных float в Go, его особенности, а также примеры использования.
---

В языке программирования Go (или Golang) тип данных `float` представляет собой один из основных типов для работы с числами с плавающей точкой. В этой статье мы рассмотрим, как использовать типы `float32` и `float64`, а также их особенности и примеры применения.

### Основные характеристики `float`

В Go типы данных с плавающей точкой представлены двумя вариантами:

- `float32` — число с плавающей точкой одинарной точности, занимает 32 бита.
- `float64` — число с плавающей точкой двойной точности, занимает 64 бита и является предпочтительным типом для большинства задач, так как обеспечивает большую точность.

`float` - один из основных числовых типов с плавающей точкой в Golang. Понимание его особенностей, точности и диапазонов значений важно для эффективной работы с числами с плавающей точкой в языке. Если вы хотите детальнее погрузиться в мир типов данных в Golang и освоить все тонкости их использования, приходите на наш курс [Основы Golang](https://purpleschool.ru/course/go-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=float_v_golang). На курсе 193 уроков и 16 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Пример использования `float`

Давайте рассмотрим пример использования типа `float64` в Go:

```go
package main

import "fmt"

func main() {
    var a float64 = 10.5
    b := 20.3
    sum := a + b

    fmt.Println("Сумма:", sum)
}
```

В этом примере мы создаем две переменные `a` и `b`, обе из которых имеют тип `float64`. Переменная `a` объявляется явно с использованием ключевого слова `var`, а переменная `b` — с помощью сокращённой формы `:=`, что позволяет Go автоматически определить тип переменной как `float64`.

### Операции с `float`

С типами `float32` и `float64` можно выполнять основные арифметические операции, такие как сложение, вычитание, умножение и деление:

```go
package main

import "fmt"

func main() {
    a := 15.7
    b := 4.2

    fmt.Println("Сложение:", a + b)
    fmt.Println("Вычитание:", a - b)
    fmt.Println("Умножение:", a * b)
    fmt.Println("Деление:", a / b)
}
```

Результатом выполнения деления `a / b` будет дробное число, так как тип `float` поддерживает значения с плавающей точкой.

### Точность и ошибки округления

При работе с типами `float32` и `float64` важно учитывать возможность ошибок округления, так как числа с плавающей точкой представляются с ограниченной точностью. Например:

```go
package main

import "fmt"

func main() {
    a := 0.1
    b := 0.2
    sum := a + b

    fmt.Println("Сумма:", sum) // Ожидается 0.3, но может быть небольшое отклонение
}
```

Из-за особенностей представления чисел с плавающей точкой в памяти, результат может содержать небольшие отклонения от ожидаемого значения.

### Работа с отрицательными числами

Типы `float32` и `float64` поддерживают работу с отрицательными значениями. Например:

```go
package main

import "fmt"

func main() {
    a := -10.5
    b := 25.3
    result := a + b

    fmt.Println("Результат:", result)
}
```

Здесь переменная `a` имеет отрицательное значение, и результат сложения также корректно отображается.

### Заключение

Типы `float32` и `float64` в Go предназначены для работы с числами с плавающей точкой. `float64` является предпочтительным типом, так как обеспечивает большую точность. При работе с числами с плавающей точкой важно учитывать возможные ошибки округления и выбирать подходящий тип данных в зависимости от задачи.

Глубокое понимание числовых типов с плавающей точкой - это основа разработки на Golang. Чтобы писать эффективный и безопасный код, необходимо хорошо понимать, как работают различные типы данных с плавающей точкой и как их правильно использовать. Все необходимые знания вы найдете на курсе [Основы Golang](https://purpleschool.ru/course/go-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=float_v_golang). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в Go прямо сегодня и станьте уверенным разработчиком.
