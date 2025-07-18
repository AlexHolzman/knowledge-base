---
metaTitle: Где хранятся данные в Docker - переменные окружения, файлы, локальные образы и учётные данные
metaDescription: Изучите, где Docker хранит данные - переменные окружения, файлы, локальные образы и учётные данные. Разберитесь в деталях хранения и управлении данными в контейнерах
author: Алексей Иванов
title: Где хранятся данные в Docker - переменные окружения, файлы, локальные образы и учётные данные
preview: Исследуйте, как и где Docker хранит важные данные - переменные окружения, файлы и образы. Мы подробно объясним процессы и предоставим примеры для лучшего понимания
---

## Введение

Понимание того, где и как Docker хранит данные, является ключевым для эффективной работы с контейнерами. Docker упрощает управление приложениями, изолируя их в контейнеры, но это также создаёт сложные ситуации с хранением данных. По мере того как вы проектируете и разворачиваете приложения, работа с переменными окружения, файлами, локальными образами и учетными данными становится неотъемлемой частью этого процесса. В данной статье мы рассмотрим, где Docker хранит эти данные и как ими можно управлять.

Docker volumes предоставляют механизм для хранения данных, но управление большим количеством контейнеров и их конфигурацией требует автоматизации. Ansible позволяет управлять конфигурацией контейнеров, развертывать приложения и обеспечивать их консистентность. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Gde_hranyatsya_dannye_v_Docker_-_peremennye_okruzheniya,_fayly,_lokalnye_obrazy_i_uchyotnye_dannye) вы научитесь управлять конфигурацией Docker-контейнеров с помощью Ansible. На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Переменные окружения

Переменные окружения играют важную роль в настройке контейнеров Docker. Они позволяют передавать значимые параметры и конфигурации в контейнеры без изменения кода приложения. Давайте посмотрим, как это работает.

### Настройка переменных окружения

Вы можете задать переменные окружения несколькими способами. Первый и самый популярный способ — это указание переменных в `Dockerfile`. Давайте посмотрим, как это делается:

```dockerfile
# Установка переменной окружения в Dockerfile
ENV API_KEY=my_secret_key
```

Этот фрагмент кода устанавливает переменную `API_KEY` со значением `my_secret_key` внутри контейнера.

Другой способ установки переменных — через команду `docker run`:

```bash
# Запуск контейнера с указанной переменной окружения
docker run -e "DB_HOST=127.0.0.1" my_container
```

Здесь `DB_HOST` будет доступен внутри контейнера с указанным значением.

### Хранение и доступ

Когда контейнер работает, переменные окружения хранятся в памяти. Это делает их очень быстрыми для доступа, но они также исчезают при остановке контейнера. Поэтому для долговременного хранения вы должны использовать другие механизмы, такие как файловые конфигурации или секреты Docker.

## Файлы и каталоги

Файлы и данные, сохранённые в контейнерах, являются важной частью работы с Docker. Давайте разберемся, где они хранятся и как можно обеспечить их сохранность.

### Волютумы и бинды

Docker предоставляет два основных механизма для хранения данных: Volumes и Bind Mounts.

#### Volumes

Volumes — это предпочтительный способ хранения данных в Docker из-за их независимости от хоста. Они хранятся в файловой системе Docker и не зависят от конкретной директории на хосте.

```bash
# Создание волюма
docker volume create my_volume

# Использование волюма в контейнере
docker run -v my_volume:/app/data my_container
```

`my_volume` здесь сохраняет данные, которые доступны в контейнере по пути `/app/data`.

#### Bind Mounts

Bind Mounts привязывают директорию на хосте к контейнеру. Это может быть полезно для разработки, где изменения на хосте должны моментально отображаться в контейнере.

```bash
# Использование bind mount
docker run -v /host/data:/app/data my_container
```

## Локальные образы

Давайте рассмотрим, где Docker хранит локальные образы, которые вы создаете или загружаете из Docker Hub.

### Каталог хранения образов

Docker хранит образы в специальном внутреннем хранилище на вашем устройстве. На Linux по умолчанию образы размещены в `/var/lib/docker`, а на Windows и MacOS — в специфичных для платформы каталогах. Образы хранятся как слои, что позволяет эффективно использовать диск и повторно использовать общий контент между несколькими образами.

### Управление образами

Чтобы получить список всех локальных образов, вы можете использовать команду:

```bash
# Получение списка локальных образов
docker images
```

Для удаления ненужных образов используйте команду:

```bash
# Удаление образа
docker rmi image_name
```

## Учётные данные

Учетные данные важны для доступа к приватным репозиториям и регистрации пользователей. Docker предоставляет инструмент Docker Secret для безопасного управления такими данными.

### Использование Docker Secrets

Docker Secrets позволяет вам безопасно хранить и управлять конфиденциальными данными. Это практично для использования в продакшн окружениях, где безопасность критически важна.

```bash
# Создание секрета
echo "my_password" | docker secret create my_password -

# Использование секрета в сервисе
docker service create --name my_service --secret my_password my_image
```

Эти секреты доступны только сервисам, которым они назначены. Это обеспечивает высокий уровень безопасности.

Работа с Docker предоставляет гибкие способы управления и размещения данных. Понимание того, где и как данные хранятся, поможет вам двигаться на шаг вперёд, обеспечивая надёжность и безопасность ваших приложений. Комплексный подход к управлению данными внутри контейнеров даёт возможность создавать устойчивые и масштабируемые системы. Для автоматизации управления инфраструктурой и развертывания приложений в больших масштабах используется Ansible. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Gde_hranyatsya_dannye_v_Docker_-_peremennye_okruzheniya,_fayly,_lokalnye_obrazy_i_uchyotnye_dannye) вы освоите Ansible и научитесь автоматизировать управление Docker-контейнерами и их данными. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир Docker и Ansible прямо сегодня.
