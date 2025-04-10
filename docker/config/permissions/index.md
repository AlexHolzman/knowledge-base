---
metaTitle: Как настроить права доступа в Docker
metaDescription: Узнайте, как правильно настроить права доступа в Docker-контейнерах чтобы обеспечить их безопасное исполнение и ограничить доступ к системе
author: Олег Марков
title: Как настроить права доступа в Docker
preview: В статье рассказывается о том как настроить права доступа в Docker-контейнерах чтобы ограничить доступ и обеспечить безопасность исполнения
---

## Введение

Добро пожаловать в мир Docker! Если вы только что начали работать с этой потрясающей технологией контейнеризации, то наверняка уже слышали о важности настройки прав доступа. Понимание и правильная настройка прав доступа в Docker-контейнерах не только обеспечивают безопасность системы, но и дают уверенность в том, что ваш контейнер работает в должных рамках. 

Давайте глубже погрузимся в процесс настройки прав доступа в Docker. Я покажу вам, как это сделать, чтобы вы могли безопасно управлять своими контейнерами.

## Права доступа в Docker

Настройка прав доступа в Docker охватывает несколько важных аспектов, таких как управление пользователями внутри контейнера, настройка капабилити (capabilities) и работа с файлами и томами. Давайте углубимся в каждый из этих аспектов.

### Управление пользователями внутри контейнера

В контейнере по умолчанию все операции выполняются от имени пользователя root. Это предоставляет максимальные привилегии, но также может создавать угрозы безопасности. Чтобы уменьшить риски, следует управлять пользователями внутри контейнера:

#### Создание пользователей и переключение между ними

В Dockerfile вы можете создать нового пользователя и переключиться на него:

```Dockerfile
# Начинаем с базового образа
FROM ubuntu:20.04

# Создаем нового пользователя с именем 'appuser'
RUN useradd -ms /bin/bash appuser

# Переключаемся на созданного пользователя
USER appuser

# Здесь все команды будут выполняться от имени 'appuser'
```

Смотрите, как просто! Теперь все команды внутри контейнера будут выполняться от имени "appuser", а не от root.

### Настройка капабилити

Docker позволяет настраивать капабилити (возможности) на уровне процессов. Это дает нам возможность удалять ненужные привилегии.

#### Удаление капабилити

С помощью команды `docker run` вы можете управлять капабилити вашего контейнера:

```bash
docker run --cap-drop NET_ADMIN --cap-drop SYS_MODULE your_image
```

Здесь мы удаляем NET_ADMIN и SYS_MODULE, чтобы контейнер не мог управлять сетевым администрированием и загружать ядро. Это значительно уменьшает поверхность для атак.

### Работа с файлами и томами

Правильная настройка доступа к файлам и томам играет ключевую роль в безопасности Docker.

#### Защита конфиденциальных файлов

Если вам нужно передать конфиденциальные данные в контейнер, рассмотрите возможность использования секретов Docker:

```bash
# Генерируем секрет
echo "my_secret_password" | docker secret create my_password -

# Запускаем контейнер с секретом
docker service create --name my_app --secret my_password my_image
```

### Управление доступом к ресурсам

#### Ограничение ресурсов контейнера

Избыток доступа может означать возможность использования лишних ресурсов, что может навредить основной системе. Для ограничения ресурсов используйте такие параметры, как `--cpus` и `--memory`:

```bash
docker run --cpus=".5" --memory="256m" your_image
```

Этот пример ограничивает контейнер 0.5 CPU и 256 MB RAM. Таким образом, контейнер не сможет использовать более ресурсов, чем установленно.

## Заключение

Теперь вы знаете, как настроить права доступа в Docker для повышения безопасности контейнеров. Используя вышеописанные методы, вы сможете регулировать доступ пользователей, управлять капабилити, защищать конфиденциальные данные и контролировать использование ресурсов. Эти знания помогут создать более защищенные и функциональные среды для ваших приложений.

Оставайтесь на связи, продолжайте изучать Docker и наслаждайтесь безопасной контейнеризацией!