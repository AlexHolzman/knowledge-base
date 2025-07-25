---
metaTitle: Запуск Python-приложений в Docker
metaDescription: Узнайте, как начать использовать Docker для запуска Python-приложений - рассмотрим создание Dockerfile, сборку образа и запуск контейнера.
author: Олег Марков
title: Запуск Python-приложений в Docker
preview: В этой статье мы разберем, как использовать Docker для запуска Python-приложений - от создания Dockerfile до запуска готового контейнера
---

## Введение

В современном мире программирования контейнеризация стала важным инструментом в управлении приложениями и их зависимостями. Она предоставляет разработчикам возможность создавать, разворачивать и управлять приложениями независимо от используемой инфраструктуры. Одним из наиболее популярных инструментов контейнеризации является Docker. С помощью Docker вы можете упаковать своё приложение и все его зависимости в единый контейнер, что облегчает его развертывание в любом окружении. В этой статье вы узнаете, как запустить Python-приложения в Docker.

## Что такое Docker и как он работает

Docker — это платформа, которая позволяет разработчикам автоматизировать развертывание приложений в контейнерах. Эти контейнеры действуют как изолированные среды, которые включают в себя всё необходимое для запуска приложения: код, runtime, библиотеки и настройки. Это позволяет создавать уверенность в том, что ваше приложение будет работать одинаково независимо от системы, на которой оно запускается.

Создание Dockerfile для Python-приложения – это важный навык, но для production-окружения этого недостаточно. Необходимо уметь автоматизировать развертывание и оркестрацию контейнеров. Если вы хотите детальнее погрузиться в Docker и научиться разворачивать Python-приложения в кластере Docker Swarm, а также автоматизировать процесс развертывания с помощью Ansible, приходите на наш большой курс [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Zapusk_Python-prilozheniy_v_Docker). На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Как установить Docker

Прежде чем мы начнем, давайте убедимся, что у вас установлен Docker. Для этого выполните следующие шаги:

1. Посетите официальный сайт Docker и загрузите установщик для вашей операционной системы.
2. Следуйте инструкциям для установки Docker Desktop.
3. После установки запустите Docker и убедитесь, что он работает, выполнив команду `docker --version` в командной строке.

### Преимущества использования Docker для Python-приложений

Запуск Python-приложений в Docker имеет несколько неоспоримых преимуществ:

- **Изоляция**: Каждое приложение работает в своей собственной средней контейнера. Это предотвращает конфликты между зависимостями и делает ваш проект более стабильным.
- **Универсальность**: Вы можете запускать ваш контейнер практически в любом месте, будь то локальная машина разработчика, тестовые серверы или облачные платформы.
- **Гибкость**: Простое управление версиями, простое обновление зависимостей и поддержка различных версий Python.

## Dockerfile и первый контейнер

Теперь, когда у вас есть общее представление о Docker, давайте перейдем к созданию Dockerfile и нашего первого контейнера.

### Создание Dockerfile

Dockerfile — это скрипт, содержащий набор инструкций по сборке Docker-образа. Это как рецепт для создания контейнера вашего приложения. Давайте создадим простой Dockerfile для Python-приложения.

Начнем с простого приложения на Python:

```python
# app.py

print("Привет, мир из Docker-контейнера!")
```

Затем создайте Dockerfile в той же директории:

```plaintext
# Используем официальный образ Python
FROM python:3.8-slim

# Устанавливаем рабочую директорию внутри контейнера
WORKDIR /app

# Копируем содержимое текущей директории в контейнер
COPY . .

# Настраиваем запуск нашего приложения
CMD ["python", "app.py"]
```

### Сборка Docker-образа

Теперь давайте соберем Docker-образ на основе нашего Dockerfile. Выполните эту команду в директории с вашим Dockerfile:

```bash
docker build -t my-python-app .
```

Здесь `-t` указывает имя нашего образа. Точка в конце команды указывает на текущую директорию как место расположения Dockerfile.

### Запуск контейнера

После успешной сборки образа, мы можем запустить наш контейнер:

```bash
docker run my-python-app
```

Если всё прошло успешно, вы должны увидеть в консоли сообщение: `Привет, мир из Docker-контейнера!`

## Работа с зависимостями и виртуальными окружениями

Теперь, давайте рассмотрим более сложный случай: когда наше приложение зависит от внешних библиотек. В Python мы обычно используем `requirements.txt` для управления зависимостями.

### Добавление зависимостей в Dockerfile

Создадим файл `requirements.txt`:

```plaintext
# requirements.txt

flask  # пример внешней библиотеки
```

Обновим наш Dockerfile, чтобы устанавливать зависимости:

```plaintext
# Используем официальный образ Python
FROM python:3.8-slim

# Устанавливаем рабочую директорию внутри контейнера
WORKDIR /app

# Копируем файлы зависимостей
COPY requirements.txt .

# Устанавливаем зависимости
RUN pip install --no-cache-dir -r requirements.txt

# Копируем всё остальное
COPY . .

# Настраиваем запуск нашего приложения
CMD ["python", "app.py"]
```

### Пересборка и запуск

После обновления Dockerfile, пересоберите образ:

```bash
docker build -t my-python-app-with-deps .
```

Теперь запустите его:

```bash
docker run my-python-app-with-deps
```

В этот раз контейнер будет содержать все необходимые зависимости для корректного выполнения вашего приложения.

Теперь, когда вы знакомы с запуском Python-приложений в Docker, вы можете использовать эту мощную платформу для управления и развертывания своих проектов. С помощью Docker вы сможете легко справляться с зависимостями, изменениями в окружении и версиями приложений. Это делает Docker неотъемлемым инструментом в арсенале современного разработчика.

Docker предоставляет уверенность в том, что ваше приложение будет работать одинаково в разных условиях. Вы можете сосредоточиться на разработке, оставив развертывание и управление окружающей средой Docker-контейнерам. Теперь, когда вы освоили основы контейнеризации с Docker, вы готовы исследовать дополнительные возможности и интеграции этого инструмента в ваших проектах. Надеюсь, эта статья была полезна, и вы сможете извлечь из неё максимум.

Запуск Python-приложений в Docker упрощает процесс разработки и деплоя, но для реальной эксплуатации требуется автоматизация. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Zapusk_Python-prilozheniy_v_Docker) вы научитесь использовать Ansible для автоматизации развертывания Docker-окружения для Python-приложений, а также познакомитесь с Docker Swarm для создания кластеров. Первые 3 модуля уже доступны бесплатно – начните погружение в мир Docker и Ansible уже сегодня.
