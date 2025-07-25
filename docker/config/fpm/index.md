---
metaTitle: Работа с php-fpm в Docker
metaDescription: Узнайте, как настроить и использовать php-fpm в Docker для оптимизации производительности веб-приложений. Эффективное развертывание PHP приложений с помощью контейнеризации.
author: Алексей Смирнов
title: Работа с php-fpm в Docker
preview: Научитесь эффективно настраивать php-fpm в Docker контейнерах. Пошаговые инструкции и практические примеры помогут вам оптимизировать работу ваших PHP-приложений.
---

## Введение

В мире веб-разработки PHP остается одним из самых популярных языков программирования. Современные веб-разработчики все чаще обращаются к контейнеризации, чтобы упростить процесс развертывания и управления приложениями. Docker позволяет изолировать приложения от инфраструктуры, обеспечивая гибкость и масштабируемость. В этой статье мы рассмотрим, как использовать PHP-FPM (FastCGI Process Manager) в Docker для оптимизации производительности PHP-приложений.

PHP-FPM — это альтернатива традиционному CGI-методу исполнения PHP. Он специально разработан для работы с веб-серверами, такими как Nginx и Apache, чтобы обрабатывать запросы более эффективно. Поддержка PHP-FPM в Docker открывает разработчикам новые возможности управления ресурсами и оптимизации производительности приложений.

Использование php-fpm в Docker позволяет оптимизировать производительность веб-приложений, обеспечивая эффективное развертывание и масштабирование. Если вы хотите детальнее погрузиться в управление инфраструктурой и развертыванием приложений в Docker — приходите на наш большой курс [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Rabota_s_php-fpm_v_Docker). На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Создание Docker-окружения для PHP-FPM

Для начала работы с PHP-FPM в Docker вам понадобится Docker и Docker Compose. Мы будем использовать Docker Compose для упрощенного управления контейнерами. Давайте создадим простое окружение:

Создайте директорию для вашего проекта и внутри нее создайте файл `docker-compose.yml`. Это основной файл, который определяет всю конфигурацию вашего Docker-окружения.

```yml
version: '3.8' # Определяем версию docker-compose

services: # Определяем сервисы
  web: 
    image: nginx:latest # Используем образ Nginx
    ports:
      - "8080:80" # Маппинг порта 8080 на 80 порт в контейнере
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf # Монтируем наш конфигурационный файл Nginx
    depends_on:
      - php

  php:
    image: php:7.4-fpm # Используем образ PHP с поддержкой FPM
    volumes:
      - ./src:/var/www/html # Монтируем директорию с PHP-кодом
```

Теперь у нас есть базовая конфигурация, состоящая из двух сервисов: Nginx и PHP-FPM. Nginx будет служить фронтендом, принимающим HTTP-запросы, а PHP-FPM будет обрабатывать PHP-код.

### Конфигурация Nginx

Создайте файл `nginx.conf` в корне директории проекта:

```nginx
server {
    listen 80; # Слушаем 80 порт

    root /var/www/html; # Корневая директория PHP-кода
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404; # Пытаемся найти запрашиваемый файл
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass php:9000; # Пробрасываем PHP-запросы на php-fpm
    }
}
```

Эта конфигурация отвечает за проксирование PHP-запросов к FPM-процессу. `fastcgi_pass php:9000;` указывает, что Nginx должен перенаправлять PHP-запросы на PHP-FPM, который находится в другом контейнере.

## Развертывание приложения

Запустите Docker Compose для создания и запуска контейнеров:

```bash
docker-compose up -d
```

Опция `-d` запускает процесс в фоновом режиме. Используя `docker-compose up`, вы создаете и запускаете оба контейнера: Nginx и PHP-FPM.

### Проверка работы

Поместите файл `index.php` в папку `src` с простым содержимым:

```php
<?php
phpinfo(); // Выводим информацию о PHP
```

Теперь откройте браузер и перейдите по адресу `http://localhost:8080`. Если все настроено правильно, вы увидите стандартную страницу PHP с информацией, которая подтверждает, что PHP-FPM обрабатывает запросы.

## Тонкая настройка PHP-FPM

PHP-FPM предоставляет множество опций для тонкой настройки производительности и управления процессами. Следующий важный шаг — изучить и оптимизировать параметры PHP-FPM в `php-fpm.conf`. Этот файл внутри контейнера можно настроить для улучшения производительности.

### Важные параметры PHP-FPM

- **pm.max_children:** определяет максимальное число дочерних процессов. Этот параметр напрямую влияет на способность сервера обрабатывать параллельные запросы. Увеличение этого значения может улучшить производительность, но увеличит использование памяти.

- **pm.start_servers:** количество процессов, запускаемых при старте. Определите это значение исходя из ожидаемого начального наплыва запросов.

- **pm.min_spare_servers** и **pm.max_spare_servers:** минимальное и максимальное число процессов, которые будут простаивать, ожидая запросы. Эти параметры помогают управлять доступностью ресурсов.

Эти параметры можно передать контейнеру через переменные среды или монтированием пользовательского `php-fpm.conf`.

### Пример монтирования пользовательского php-fpm.conf

Создайте файл `php-fpm.conf` и добавьте параметры, исходя из особенностей вашего приложения. После этого обновите конфигурацию в `docker-compose.yml`:

```yml
  php:
    image: php:7.4-fpm
    volumes:
      - ./src:/var/www/html
      - ./php-fpm.conf:/usr/local/etc/php-fpm.d/www.conf # Монтируем наш конфигурационный файл PHP-FPM
```

## Заключение

Объединение Docker и PHP-FPM позволяет разрабатывать и развертывать PHP-приложения быстро и эффективно. Контейнеризация обеспечивает изоляцию приложений, легкость управления зависимостями и масштабируемость. Настройка PHP-FPM повышает производительность, и в это сыграет значительную роль тонкая настройка параметров, адаптированная под уникальные требования вашего проекта. Овладев навыками контейнеризации с помощью Docker и PHP-FPM, вы сможете значительно упростить процесс управления и развертывания ваших PHP-приложений.

Развертывание PHP приложений с помощью php-fpm в Docker позволяет повысить производительность и упростить управление. Для автоматизации процессов развертывания и управления контейнерами необходимы инструменты оркестрации и автоматизации. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Rabota_s_php-fpm_v_Docker) вы научитесь использовать Ansible для автоматизации Docker, управлять Docker Swarm кластерами и создавать полноценные CI/CD пайплайны. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир Docker прямо сегодня и узнайте, как автоматизировать развертывание и управление контейнерами.
