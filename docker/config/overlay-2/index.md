---
metaTitle: Что такое overlay2 storage driver в Docker
metaDescription: Узнайте, как overlay2 storage driver в Docker позволяет эффективно работать с файловыми системами контейнеров, изучите его возможности и конфигурацию
author: Олег Марков
title: Что такое overlay2 storage driver в Docker
preview: Исследуйте overlay2 storage driver в Docker - как он работает, зачем нужен и какие преимущества предоставляет для контейнеров. Примеры и пояснения помогут вам быстро освоить его
---

## Введение

Docker — это платформа контейнеризации, которая позволяет разработчикам упаковывать приложения и их зависимости в контейнеры, которые могут быть легко развёрнуты где угодно. Одной из ключевых технологий, которая делает контейнеры таковыми, является драйвер хранения. Docker обеспечивает несколько вариантов использования различных драйверов хранения для управления файлами в контейнерах, но на данный момент наиболее популярным и рекомендованным является драйвер `overlay2`.

## Введение в Overlay2 Storage Driver

### Что такое Overlay2?

`Overlay2` — это улучшенная версия драйвера `overlay`, использующего механизм наложения файловых систем. Она предоставляет возможность слоям файловой системы "перекрывать" друг друга. Этот подход реализует концепцию образов и контейнеров, где образы состоят из нескольких слоев, а все изменения, которые делает контейнер, происходят в верхнем слое или слое "наложения".

Overlay2 storage driver является одним из наиболее распространенных драйверов хранения в Docker, обеспечивающим эффективную работу с файловой системой контейнера. Понимание его особенностей важно для оптимизации производительности. Если вы хотите детальнее погрузиться в управление инфраструктурой и развертыванием приложений в Docker — приходите на наш большой курс [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Chto_takoe_overlay2_storage_driver_v_Docker). На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Как это работает?

Каждый образ Docker состоит из слоев. Эти слои читаются контейнерами и в идеале не изменяются. Однако, контейнеры должны иметь возможность вносить изменения в файловую систему, например, для записи логов или создания временных файлов. Вот здесь и вступает в игру `overlay2`, предоставляя механизм для изолирования этих изменений.

В `overlay2` используется три основных компонента:

- **LowerDir** — содержит оригинальные неизменяемые данные образа.
- **UpperDir** — хранит изменения, которые были внесены в контейнер.
- **WorkDir** — временное местоположение для обработки изменений, когда контейнер вносит изменения в UpperDir.

Когда изменения сделаны, они сохраняются в UpperDir, который рассматривается как новое состояние файловой системы контейнера.

## Преимущества использования Overlay2

### Эффективность пространства

Благодаря концепции слоев, `overlay2` позволяет повторно использовать части образов, что значительно экономит пространство на диске. Удаление файла из контейнера или добавление нового — это операция на верхнем слое, в то время как базовые слои остаются неизменными.

### Быстродействие

Работа с `overlay2` не требует копирования большого объема данных, чтобы начать работу с контейнером. Это делает запуск контейнеров быстрее по сравнению с традиционными методами, такими как полное копирование образов.

### Поддержка многослойности

`Overlay2` успешно справляется с многочисленными слоями образов, что полезно для сложных приложений с многослойными архитектурами.

### Упрощенная логика

`Overlay2` использует простую, но мощную модель наложения слоев. Это означает, что пользователям и администраторам легко понять, как данные обрабатываются и изменяются в контейнерах.

## Настройка Overlay2

### Установка Docker с Overlay2

По умолчанию Docker на большинстве систем уже использует `overlay2` для управления хранилищем контейнеров. Однако, в некоторых случаях может потребоваться его явная настройка.

#### Проверка текущего драйвера

Чтобы узнать, какой драйвер хранения используется в вашей установке Docker, выполните команду:

```bash
docker info | grep "Storage Driver"
```

Вы увидите что-то вроде:

```
Storage Driver: overlay2
```

#### Переключение на Overlay2

Если ваш Docker не использует `overlay2` и вы хотите сменить драйвер, выполните следующие шаги:

1. Остановите все работающие контейнеры и остановите службу Docker с помощью:

   ```bash
   sudo systemctl stop docker
   ```

2. Отредактируйте файл конфигурации Docker, который обычно находится по пути `/etc/docker/daemon.json`. Добавьте или измените запись `"storage-driver"`:

   ```json
   {
     "storage-driver": "overlay2"
   }
   ```

3. Перезагрузите Docker:

   ```bash
   sudo systemctl start docker
   ```

4. Проверьте, что изменения вступили в силу, снова выполнив:

   ```bash
   docker info | grep "Storage Driver"
   ```

Теперь давайте рассмотрим несколько примеров, чтобы уверенно настроить Overlay2 в реальных сценариях.

## Примеры использования Overlay2

### Ускоренный запуск контейнеров

Благодаря `overlay2`, Docker может быстрее запускать контейнеры, поскольку нет необходимости копировать весь образ в файловую систему. Обратите внимание, как происходит запуск, используя пример.

```bash
docker run -d nginx
```

В этом примере контейнер запускается в считанные секунды, поскольку `overlay2` обрабатывает слои директории образов и не требует полного копирования.

### Изоляция изменений

Представьте, что вам нужно протестировать изменения в файлах конфигурации вашего приложения:

```bash
docker run -it myapp bash
# Внутри контейнера измените конфигурацию
vi /app/config/settings.yml
```

Изменения сохраняются в `UpperDir` и не влияют на оригинальный образ, что позволяет вам безопасно экспериментировать с конфигурациями.

Касаясь этих аспектов, `overlay2` значительно упрощает работу с Docker на уровне файловой системы и делает контейнеризацию более простой и эффективной.

Overlay2 является предпочтительным выбором для современных разработчиков, работающих с Docker, благодаря своей простоте, скорости и эффективности в управлении файлами. Это основа, на которой строятся современные контейнерные приложения, и важно понимать, как она работает, чтобы эффективно использовать все преимущества контейнеризации.

Выбор и настройка storage driver в Docker является важным аспектом для обеспечения оптимальной производительности. Для автоматизации процессов развертывания и управления контейнерами необходимы инструменты оркестрации и автоматизации. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Chto_takoe_overlay2_storage_driver_v_Docker) вы научитесь использовать Ansible для автоматизации Docker, управлять Docker Swarm кластерами и создавать полноценные CI/CD пайплайны. Начните свое обучение с 3 бесплатными модулями прямо сейчас.
