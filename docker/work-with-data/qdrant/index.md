---
metaTitle: Работа с Qdrant в Docker
metaDescription: Узнайте, как эффективно разворачивать и использовать Qdrant в Docker для управления и поиска векторных данных с высокой производительностью
author: Алексей Иванов
title: Работа с Qdrant в Docker
preview: Откройте для себя процесс настройки и эксплуатации Qdrant в Docker-среде для управления векторными данными. Шаги установки, примеры и советы помогут вам в этом
---

## Введение

Qdrant – это современный движок для векторного поиска и управления, предназначенный для оптимизации работы с высокоразмерными векторами. Благодаря этому инструменту, вы сможете эффективно обрабатывать и искать вектора, что особенно актуально в эпоху машинного обучения и искусственного интеллекта. Docker, в свою очередь, упрощает процесс развертывания таких приложений, обеспечивая им изоляцию и легкую масштабируемость. В этой статье мы рассмотрим, как использовать Qdrant в Docker, чтобы быстро и эффективно интегрировать возможности векторного поиска в ваши проекты.

## Установка Qdrant с использованием Docker

### Подготовка к установке

Прежде чем мы начнем, убедитесь, что у вас установлен Docker. Если это не так, вы можете скачать и установить Docker, следуя официальной документации на веб-сайте Docker. Docker сделает процесс развертывания Qdrant намного проще и эффективнее.

Развертывание Qdrant в Docker - это отличное начало, но для полноценной работы с контейнерами и их автоматизации часто требуются дополнительные инструменты. Если вы хотите научиться оркестровать контейнеры, автоматизировать деплой и познакомиться с инструментами, которые позволяют управлять Docker-окружением, обратите внимание на связку Docker и Ansible. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Rabota_s_Qdrant_v_Docker) мы подробно рассматриваем эти технологии и учим применять их на практике. На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Запуск контейнера Qdrant

Docker позволяет быстро запустить Qdrant, используя образ из Docker Hub. Давайте начнем с команды, которая загрузит и запустит для вас Qdrant:

```bash
docker run -p 6333:6333 qdrant/qdrant
```

Эта команда делает следующее:

- `docker run` – команда для запуска нового контейнера.
- `-p 6333:6333` – опция перенаправления порта. Она связывает порт 6333 на вашей машине с портом 6333 в контейнере Qdrant, таким образом вы сможете обращаться к Qdrant из вашей системы.
- `qdrant/qdrant` – это указание на образ Qdrant, который будет использоваться для создания контейнера.

### Проверка работы Qdrant

После запуска Qdrant в Docker, стоит проверить его работоспособность. Вы можете использовать команду `curl`, чтобы отправить простой запрос к Qdrant и убедиться, что он работает:

```bash
curl http://localhost:6333/collections
```

Результат должен вернуть пустой список коллекций:

```json
{
  "result": [],
  "status": "ok",
  "time": 0.000123
}
```

## Основные функции Qdrant

### Создание коллекций

Коллекции в Qdrant – это контейнеры для ваших векторных данных. Каждая коллекция может хранить векторы, и вы можете управлять ими с помощью API. Давайте создадим простую коллекцию:

```bash
curl -X POST 'http://localhost:6333/collections' \
-H 'Content-Type: application/json' \
-d '{
    "name": "my_collection",
    "vector_size": 512,
    "distance": "Cosine"
}'
```

В этом примере создана коллекция с названием `my_collection`, ожидающая векторы размером 512, которая будет использовать косинусное расстояние для измерения близости между векторами.

### Добавление векторов

После создания коллекции следующим шагом будет добавление векторов. Давайте добавим векторы в нашу коллекцию:

```bash
curl -X POST 'http://localhost:6333/collections/my_collection/points' \
-H 'Content-Type: application/json' \
-d '{
    "points": [
        {
            "id": 1,
            "vector": [0.1, 0.2, 0.3, ..., 0.512]
        },
        {
            "id": 2,
            "vector": [0.5, 0.9, 0.4, ..., 0.623]
        }
    ]
}'
```

Каждый вектор имеет уникальный идентификатор и сам вектор, который вы передаете массивом значений.

### Поиск векторов

Одной из главных возможностей Qdrant является его быстрый и эффективный векторный поиск. Теперь, когда мы добавили векторы, давайте попробуем выполнить простой поиск:

```bash
curl -X POST 'http://localhost:6333/collections/my_collection/points/search' \
-H 'Content-Type: application/json' \
-d '{
    "vector": [0.1, 0.2, 0.3, ..., 0.512],
    "top": 2
}'
```

Этот запрос попытается найти два наиболее близких вектора в коллекции `my_collection` по заданному вектору.

## Заключение

Вы изучили основы развертывания Qdrant в Docker и получили представление о его основных функциях: создании коллекций, добавлении и поиске векторов. Docker делает управление Qdrant простым и удобным, обеспечивая гибкость и масштабируемость. Теперь вы готовы использовать Qdrant в собственных проектах, извлекая пользу из мощного векторного поиска и управления данными.

Эффективное развертывание Qdrant в Docker – это только часть процесса. Для создания надежной инфраструктуры необходимо понимать принципы оркестрации и уметь автоматизировать задачи. На курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Rabota_s_Qdrant_v_Docker) вы научитесь использовать Ansible для автоматизации настройки Docker-окружения, а также освоите Docker Swarm для создания кластеров и масштабирования приложений. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир Docker и Ansible прямо сегодня.
