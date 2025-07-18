---
metaTitle: Команда ls в Docker
metaDescription: Узнайте, как использовать команду ls в Docker для управления контейнерами и образами. Изучите синтаксис и примеры использования этой команды.
author: Иван Иванов
title: Команда ls в Docker
preview: Поймите основные аспекты использования команды ls в Docker - от отображения списка контейнеров до работы с образами. Примеры и пояснения помогут вам быстро освоить эту полезную команду.
---

## Введение

В мире Docker команда `ls` является одной из наиболее полезных и практичных при управлении контейнерами и образами. Как и в традиционных операционных системах, команда `ls` в Docker выполняет функцию отображения списка, однако здесь она имеет свои особенности и полезные возможности. Это мощный инструмент, который поможет вам управлять Docker-контейнерами и образами более эффективно. Давайте рассмотрим, как эта команда используется в Docker и какие задачи она позволяет решать.

### Почему важно изучить команду ls в Docker

Перед тем как углубляться в детали, стоит понимать, зачем вообще может понадобиться использовать команду `ls` в Docker. Эта команда позволяет пользователям быстро получить информацию о различных объектах в Docker: контейнерах, образах, сетях, томах и многом другом. Зная, как правильно применять `ls`, вы сможете быстрее и эффективнее анализировать текущее состояние вашего Docker-средовища.

Использование команды `ls` в Docker позволяет управлять контейнерами и образами, просматривая их содержимое. Это важный инструмент для навигации и управления файлами в Docker. Если вы хотите детальнее погрузиться в вопросы управления контейнерами и образами в Docker, а также узнать, как использовать команду `ls` для этого, приходите на наш большой курс [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Komanda_ls_v_Docker). На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Использование команды ls в Docker

Команда `ls` в Docker используется совместно с различными объектами Docker. Смотрите, я покажу вам несколько примеров и объясню, как это работает на практике.

### Список контейнеров

Чтобы получить список всех контейнеров, вы можете использовать команду:

```bash
docker container ls
```

По умолчанию эта команда отобразит список только работающих контейнеров. Чтобы увидеть все контейнеры, включая остановленные, добавьте флаг `-a`:

```bash
docker container ls -a
```

#### Пример

```bash
# Покажем все контейнеры
docker container ls -a

# Выход может быть таким:
# CONTAINER ID   IMAGE          COMMAND       CREATED        STATUS                    PORTS      NAMES
# 4c01db0b339c   ubuntu:latest  "/bin/bash"   5 hours ago    Exited (0) 4 hours ago              upbeat_sinoussi
```

### Список образов

Для управления образами Docker также предоставляет команду `ls`:

```bash
docker image ls
```

Эта команда отображает все доступные образы вместе с информацией о тегах, размере и других параметрах.

#### Пример

```bash
docker image ls

# Вывод может выглядеть так:
# REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
# ubuntu        latest    5fbb6b3cdc64   2 weeks ago    72.9MB
```

### Список сетей

Docker позволяет создавать и управлять сетями, в которых работают контейнеры. Чтобы увидеть текущие сети, используется следующая команда:

```bash
docker network ls
```

#### Пример

```bash
docker network ls

# Пример вывода:
# NETWORK ID     NAME                DRIVER    SCOPE
# 0b8c4a983c0e   bridge              bridge    local
# 14c3ab3bd388   none                null      local
```

### Список томов

Docker поддерживает создание томов для сохранения данных. Узнать больше о существующих томах можно с помощью команды:

```bash
docker volume ls
```

#### Пример

```bash
docker volume ls

# Вывод может быть таким:
# DRIVER    VOLUME NAME
# local     my_volume
```

## Заключение

Освоение команды `ls` в Docker является важным шагом для эффективного управления вашим Docker-средой. Эта команда позволяет быстро получать информацию о контейнерах, образах, сетях и томах, что в свою очередь упрощает мониторинг и управление ресурсами приложения. Примеры, представленные в статье, помогут вам лучше понять, как использовать команду `ls` для решения повседневных задач при работе с Docker. Не забывайте, что реальная практика и регулярное использование улучшат ваши навыки работы с Docker.

Использование `ls` — это базовый навык для работы с файлами в Docker. Для более продвинутого управления необходимо освоить Docker Compose и инструменты автоматизации. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Komanda_ls_v_Docker) вы научитесь всему необходимому для работы с Docker, включая инструменты для автоматизации управления файлами и образами. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир Docker прямо сегодня и станьте экспертом.
