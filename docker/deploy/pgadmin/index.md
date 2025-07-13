---
metaTitle: Развертывание pgadmin в Docker
metaDescription: Узнайте, как развернуть pgadmin в Docker для эффективного управления PostgreSQL базами данных, изучите шаги настройки и запуска контейнеров
author: Олег Марков
title: Развертывание pgadmin в Docker
preview: Исследуйте процесс развертывания pgadmin в Docker - начиная с настройки контейнеров и до управления PostgreSQL базами данных. Следуйте простым шагам для быстрого и удобного запуска
---

## Введение

PostgreSQL является одной из наиболее популярных систем управления базами данных благодаря своей надежности и мощным возможностям. Но для управления БД удобно использовать визуальный инструмент. PgAdmin - это один из самых распространенных веб-интерфейсов для управления PostgreSQL. В данной статье мы рассмотрим, как развернуть pgAdmin с использованием Docker, что позволяет легко и быстро настроить его на любой системе, не тратя время на сложную установку и настройку.

## Что такое Docker и почему он полезен?

Docker является платформой для автоматизации развертывания приложений в контейнерах. Контейнеры изолируют приложения друг от друга, позволяя запускать их независимо от окружающей среды. Это значительно упрощает развертывание и управление различными сервисами. Использование Docker позволяет вам собрать все необходимые зависимости и библиотеки в один контейнер, который будет одинаково работать на любых системах, поддерживающих Docker.

Развертывание pgAdmin в Docker упрощает управление базами данных PostgreSQL, но для обеспечения отказоустойчивости и автоматизации требуется оркестрация. Если вы хотите детальнее погрузиться в Docker и научиться автоматизировать настройку pgAdmin с помощью Ansible, а также создавать кластеры pgAdmin в Docker Swarm, приходите на наш большой курс [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Razvertyvanie_pgadmin_v_Docker). На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

Теперь, когда у вас есть представление о Docker, давайте перейдем к следующему шагу - развертыванию pgAdmin в Docker.

## Установка Docker

Если у вас еще не установлен Docker, теперь самое время это сделать. Установка Docker довольно проста и зависит от вашей операционной системы. Вот несколько общих шагов для установки Docker:

### Установка Docker на Windows или MacOS

1. Перейдите на официальный сайт Docker и скачайте Docker Desktop.
2. Установите загруженный файл, следуя инструкциям установщика.
3. После установки запустите Docker Desktop и убедитесь, что он работает.

### Установка Docker на Linux

1. Откройте терминал и выполните следующие команды для обновления пакетов и установки необходимых зависимостей:
   ```bash
   sudo apt-get update
   sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
   ```

2. Добавьте официальный Docker GPG ключ:
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```

3. Добавьте репозиторий Docker в ваш системный источник пакетов:
   ```bash
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```

4. Установите Docker:
   ```bash
   sudo apt-get update
   sudo apt-get install docker-ce
   ```

После установки проверьте её успешность, выполнив команду `docker --version`. Если установка завершилась успешно, вы увидите версию установленного Docker.

## Развертывание pgAdmin в Docker

Теперь мы готовы развернуть pgAdmin. Давайте начнем с создания Docker контейнера для pgAdmin.

### Создание Docker контейнера для pgAdmin

1. Сначала создайте сеть Docker для связи pgAdmin с вашими контейнерами PostgreSQL:
   ```bash
   docker network create pgnetwork
   ```

2. Теперь запустите контейнер pgAdmin, используя официальный образ `dpage/pgadmin4`:

   ```bash
   docker run --name pgadmin -p 80:80 \
     -e "PGADMIN_DEFAULT_EMAIL=user@example.com" \
     -e "PGADMIN_DEFAULT_PASSWORD=securepassword" \
     -d --network=pgnetwork dpage/pgadmin4
   ```

   Здесь:
   - `--name pgadmin` называет ваш контейнер pgAdmin.
   - `-p 80:80` связывает порт 80 вашего хоста с портом 80 контейнера, на котором будет работать pgAdmin.
   - `-e "PGADMIN_DEFAULT_EMAIL=user@example.com"` задает email для входа в pgAdmin.
   - `-e "PGADMIN_DEFAULT_PASSWORD=securepassword"` устанавливает пароль для входа.
   - `--network=pgnetwork` подключает контейнер к ранее созданной сети.
   - `dpage/pgadmin4` указывает, какой образ Docker использовать.

Посетите ваш браузер и перейдите по адресу `http://localhost`, чтобы получить доступ к веб-интерфейсу pgAdmin. Введите указанные email и пароль для входа.

### Подключение pgAdmin к базе данных PostgreSQL

Теперь, когда мы успешно развернули pgAdmin, пора подключить его к вашей базе данных PostgreSQL. Убедитесь, что ваша база данных работает на том же Docker сети `pgnetwork`. Например, если вы уже развернули PostgreSQL контейнер:

```bash
docker run --name postgresdb -e POSTGRES_PASSWORD=mysecretpassword -d --network=pgnetwork postgres
```

Теперь перейдите в интерфейс pgAdmin, добавьте новое подключение:
1. Перейдите в "Object" -> "Create" -> "Server".
2. Во вкладке "General" введите имя сервера.
3. На вкладке "Connection" введите следующую информацию:
   - Host name/address: `postgresdb` (это имя вашего PostgreSQL контейнера).
   - Port: `5432`.
   - Maintenance database: `postgres`.
   - Username: `postgres`.
   - Password: `mysecretpassword`.

После успешного подключения к базе данных вы сможете управлять вашей базой данных через pgAdmin.

## Заключение

Использование Docker для развертывания pgAdmin и PostgreSQL обеспечивает гибкость и удобство, освобождая вас от проблем с зависимостями и настройками. Вы теперь умеете развертывать pgAdmin в Docker, и это позволит вам сосредоточиться на более продуктивной работе с вашими данными. Используя эту методологию, вы заметите, насколько проще и быстрее становятся процессы развертывания и управления базами данных.

Развертывание pgAdmin в Docker упрощает процесс, но для production-окружения нужна автоматизация. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Razvertyvanie_pgadmin_v_Docker) вы научитесь использовать Ansible для автоматической настройки pgAdmin и Docker Swarm для создания отказоустойчивого кластера. Начните погружение с бесплатных модулей уже сегодня.
