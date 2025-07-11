---
metaTitle: Работа с переменными окружения (env) в Golang
metaDescription: Узнайте, как работать с переменными окружения в Go - от получения до установки значений с примерами кода и практическими советами
author: Олег Марков
title: Работа с переменными окружения (env) в Golang
preview: Погрузитесь в мир переменных окружения в Go - изучите, как получать и устанавливать значения, и узнайте о лучших практиках использования в реальных проектах
---

## Введение

Работа с переменными окружения является важной частью разработки на любом языке программирования, позволяя вашему приложению взаимодействовать с внешними системными настройками. Golang, или просто Go, предоставляет весьма понятный и удобный интерфейс для работы с этими переменными, что делает их использование легким и интуитивно понятным. 

В этой статье я покажу вам, как переменные окружения работают в Go, какие функции можно использовать для их управления и как они могут облегчить вашу жизнь как разработчика. Вы получите практические советы и примеры кода, которые помогут вам быстро освоить этот аспект программирования на Go.

Переменные окружения позволяют конфигурировать приложения без изменения кода, что критически важно для развертывания в различных окружениях. Чтобы эффективно работать с переменными окружения в Go, необходимо понимать, как их использовать для хранения секретов, как передавать их в Docker-контейнеры и как настраивать различные окружения для разработки, тестирования и продакшена. Если вы хотите детальнее погрузиться в backend разработку на Go — приходите на наш большой курс [Основы Golang](https://purpleschool.ru/course/go-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=rabota-s-peremennymi-okruzheniya-env-v-golang). На курсе 193 уроков и 16 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Получение переменных окружения

Начнем с самого простого - получения значений переменных окружения. В Go вы можете легко сделать это с помощью функции `os.Getenv`. Давайте взглянем на пример, чтобы понять, как это работает.

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	// Получаем переменную окружения PATH
	path := os.Getenv("PATH")
	
	// Выводим значение переменной PATH
	fmt.Println("Path:", path)
}
```

В этом примере мы используем `os.Getenv`, чтобы получить значение переменной окружения `PATH`. Если такая переменная не существует, `os.Getenv` вернет пустую строку.

### Обработка значения по умолчанию

Естественно, не всегда переменная окружения может быть установлена. В таких случаях можно задать значение по умолчанию, используя условие `if`.

```go
func getOrDefault(varName string, defaultValue string) string {
	value := os.Getenv(varName)
	if value == "" {
		return defaultValue
	}
	return value
}

func main() {
	// Устанавливаем значение по умолчанию для переменной APP_ENV
	appEnv := getOrDefault("APP_ENV", "development")
	fmt.Println("App Environment:", appEnv)
}
```

Таким образом, если переменная окружения `APP_ENV` не установлена, ваша программа будет использовать значение по умолчанию "development". Этот подход весьма полезен для разработчиков, которые хотят обеспечить надежное поведение приложений даже в непредсказуемой среде.

## Установка переменных окружения

Теперь давайте разберемся, как устанавливать переменные окружения в Go. Этим занимается функция `os.Setenv`. Очень важно отметить, что изменения, сделанные с помощью `os.Setenv`, ограничены лишь текущим процессом и его потомками. Они не будут видны другим процессам или сессиям.

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	// Устанавливаем значение переменной окружения DATABASE_URL
	err := os.Setenv("DATABASE_URL", "postgres://user:password@localhost/db")
	if err != nil {
		fmt.Println("Error setting environment variable:", err)
	}
	
	// Проверяем, что переменная была установлена
	dbUrl := os.Getenv("DATABASE_URL")
	fmt.Println("Database URL:", dbUrl)
}
```

Как видно из примера, функция `os.Setenv` возвращает ошибку, которую стоит обрабатывать, чтобы быть уверенным в корректности изменений.

## Удаление переменных окружения

Иногда возникает необходимость удалить переменную окружения. Для этого существует функция `os.Unsetenv`.

```go
package main

import (
	"fmt"
	"os"
)

func main() {
	// Устанавливаем, а затем удаляем переменную окружения TEST_VAR
	os.Setenv("TEST_VAR", "some_value")
	err := os.Unsetenv("TEST_VAR")
	if err != nil {
		fmt.Println("Error unsetting environment variable:", err)
	}

	// Проверяем, что переменная была удалена
	testVar := os.Getenv("TEST_VAR")
	fmt.Println("Test Variable:", testVar) // Должен вывести пустую строку
}
```

При использовании `os.Unsetenv` также стоит обрабатывать ошибки, чтобы знать, что переменная действительно удалена.

## Заключение

Работа с переменными окружения в Go проста и интуитивно понятна. Мы рассмотрели ключевые функции: `os.Getenv` для получения, `os.Setenv` для установки и `os.Unsetenv` для удаления переменных окружения. Каждый из этих элементов играет важную роль в создании надежных и адаптивных приложений. Надо отметить, что успешное использование переменных окружения делает ваш код более гибким и безопасным, позволяя адаптироваться к различным условиям без изменения кода. Надеюсь, теперь вам станет проще работать с переменными окружения в Golang, и эти знания будут полезны в ваших проектах.

Теперь вы знаете, как работать с переменными окружения в Golang. Чтобы систематизировать свои знания Go и научиться писать чистый и поддерживаемый backend код, обратите внимание на курс [Основы Golang](https://purpleschool.ru/course/go-basics?utm_source=knowledgebase&utm_medium=text&utm_campaign=rabota-s-peremennymi-okruzheniya-env-v-golang). В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в Go прямо сегодня и станьте уверенным разработчиком.
