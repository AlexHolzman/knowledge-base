---
metaTitle: Чистая архитектура в Golang
metaDescription: Погрузитесь в мир чистой архитектуры при разработке на Go - узнайте, как разделение уровней помогает писать более тестируемый и поддерживаемый код
author: Олег Марков
title: Чистая архитектура в Golang
preview: Изучите принципы чистой архитектуры с кодовыми примерами на Golang и узнайте, как они помогают создавать поддерживаемые приложения
---

## Введение

Приветствую вас в мире чистой архитектуры! Если вы уже сталкивались с такими проблемами, как сложность в изменении кода, трудности с тестированием или просто хотите улучшить структуру вашего проекта, то вы на правильном пути. Давайте разберемся, как чистая архитектура, применяемая в разрабатываемых на Golang приложениях, может помочь вам в решении этих задач.

Чистая архитектура — это подход к построению программного обеспечения, который предоставляет четкое разделение ответственности и минимизирует зависимость между компонентами. Основная цель — облегчить изменения и тестирование кода, сохраняя структуру проекта чистой и понятной.

## Основные концепции чистой архитектуры

### Разделение уровней

Чистая архитектура основана на принципах, которые позволяют делить программу на уровни. Эти уровни представляют различные степени абстракции и ответственности. Наиболее часто выделяются три основных уровня: 

- **Доменная логика** - это сердце вашей программы, где расположены правила и бизнес-логика.
- **Интерфейсы** - это слой, обеспечивающий пути коммуникации между вашим приложением и внешним миром.
- **Инфраструктура** - здесь находятся детали реализации, такие как работа с базой данных или взаимодействие с веб-сервисами.

Как это может быть представлено в коде? Давайте посмотрим:

#### Пример с использованием интерфейсов

```go
// UserRepository определяет операции для работы с пользователями
type UserRepository interface {
    Save(user User) error
    FindByID(id string) (User, error)
}

// User - это доменная модель
type User struct {
    ID   string
    Name string
}
```

В данном примере `UserRepository` определяет набор операций, которые можно выполнять с пользователями. Это интерфейс, из которого ваш код может взаимодействовать с базой данных или другим постоянным хранилищем.

### Инверсия управления

Инверсия управления (IoC) — это принцип, согласно которому выполнение программы контролируется не статическими вызовами, а внешним кодом. В контексте чистой архитектуры это позволяет изолировать доменную логику от зависимостей. 

Попробую объяснить это на примере:

```go
// UserDataStore - здесь реализована логика хранения данных
type UserDataStore struct{}

func (uds *UserDataStore) Save(user User) error {
    // Логика сохранения пользователя в базу данных
    return nil
}

func main() {
    var userRepo UserRepository
    userRepo = &UserDataStore{}  // Инжектируем зависимость

    user := User{ID: "123", Name: "Иван"}
    err := userRepo.Save(user)   // Используем интерфейс для выполнения операции
    if err != nil {
        log.Fatal(err)
    }
}
```

Здесь наш `main()` создает объект `UserDataStore`, который соответствует интерфейсу `UserRepository`, и использует его для сохранения пользователя. Это позволяет легко заменить `UserDataStore` на другую имплементацию без изменения вашего приложения.

### Принцип зависимости

Этот принцип гласит, что зависимости должны указывать на более высокоуровневые политики, а не на детали реализации. Это означает, что низкоуровневые компоненты должны зависеть от абстракций.

#### Пример зависимости

```go
// PaymentService определяет операции для работы с платежами
type PaymentService interface {
    Charge(amount float64) error
}

// PaymentProcessor - это низкоуровневый компонент
type PaymentProcessor struct{}

func (pp *PaymentProcessor) Charge(amount float64) error {
    // Исполнение операции платежа
    return nil
}

type OrderService struct {
    payment PaymentService  // Зависимость от интерфейса, а не реализации
}

func (os *OrderService) CompleteOrder(amount float64) error {
    return os.payment.Charge(amount)  // Используем интерфейс
}
```

В этом примере `OrderService` не зависит от конкретной реализации `PaymentProcessor`, а только от интерфейса `PaymentService`. Это позволяет менять реализацию платежного сервиса без изменения логики обработки заказов.

## Заключение

Чистая архитектура — это методология, которая помогает нам управлять сложностью больших систем. Разделение ответственности, инверсия управления и зависимость от абстракций делают наш код более гибким и удобным для тестирования. Я искренне надеюсь, что вы нашли эту статью полезной и теперь лучше понимаете, как применить эти принципы в своих проектах на Golang. Успехов в разработке!