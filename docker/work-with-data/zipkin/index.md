---
metaTitle: Трассировка запросов с помощью Zipkin в Docker
metaDescription: Узнайте, как использовать Zipkin для трассировки запросов в Docker-среде - шаги настройки, возможности и преимущества
author: Олег Марков
title: Трассировка запросов с помощью Zipkin в Docker
preview: Изучите процесс трассировки запросов в Docker с помощью Zipkin - от установки до примеров использования для эффективного мониторинга и улучшения производительности ваших приложений
---

## Введение

В современном мире микросервисной архитектуры управление и отслеживание запросов становится важной задачей для обеспечения стабильности и оптимальной работы приложений. Одним из мощных инструментов для выполнения этой задачи является Zipkin. Он предоставляет возможность детальной трассировки запросов в распределённых системах. Сегодня я расскажу вам, как интегрировать Zipkin в среду Docker и использовать его для подробного мониторинга запросов, проходящих через ваши сервисы.

## Установка и настройка Zipkin в Docker

Zipkin — это система распределённого трейсинга, которая помогает разработчикам диагностировать проблемы и оптимизировать производительность своих приложений. Давайте разберёмся, как его установить в контейнеризированной среде Docker.

Для более глубокого понимания работы Docker-контейнеров и организации эффективного мониторинга, трассировки и логирования, необходимо освоить широкий спектр инструментов и техник. Если вы хотите детальнее погрузиться в Docker — приходите на наш большой курс [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Trassirovka_zaprosov_s_pomoshchyu_Zipkin_v_Docker
). На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами. На курсе вы освоите базовые понятия Docker, работу с образами, сетями и томами, а также научитесь использовать Docker-compose для управления мультиконтейнерными приложениями.

### Шаг 1: Запуск Zipkin-контейнера

Запустить Zipkin в Docker достаточно просто. Используется официальный образ, который содержит все необходимые зависимости. Давайте посмотрим, как это сделать.

```bash
docker run -d -p 9411:9411 openzipkin/zipkin
```

В этой команде `docker run` инструмент Docker, который запускает контейнеры. Опция `-d` означает, что контейнер будет запущен в фоновом режиме. Порт `9411` - это стандартный порт, используемый Zipkin для коммуникации.

### Шаг 2: Проверка работы Zipkin

После запуска контейнера вы можете проверить, работает ли Zipkin, перейдя на `http://localhost:9411` в вашем браузере. Если всё настроено правильно, вы должны увидеть пользовательский интерфейс Zipkin, готовый к работе.

## Интеграция Zipkin с вашими приложениями

Для того чтобы ZIPkin мог собирать и анализировать данные, необходимо интегрировать его клиентскую библиотеку с вашими сервисами. Это можно сделать разными способами в зависимости от используемого вами языка программирования и инфраструктуры.

### Инструменты интеграции

Zipkin предоставляет множество клиентских библиотек и инструментов для различных языков программирования. Самые популярные из них:

- Brave для Java
- zipkin-go для Go
- zipkin-ruby для Ruby
- zipkin-js для JavaScript

Давайте рассмотрим, как интеграция может выглядеть на примере Java-приложения с использованием библиотеки Brave.

#### Интеграция с Java-приложением

Для начала необходимо добавить зависимость к вашему `pom.xml`, если вы используете Maven:

```xml
<dependency>
    <groupId>io.zipkin.brave</groupId>
    <artifactId>brave-core</artifactId>
    <version>5.12.3</version>
</dependency>
```

Теперь давайте настроим приложение для отправки данных о трейсинге в Zipkin.

```java
Tracing tracing = Tracing.newBuilder()
        .localServiceName("your-service-name") // Имя вашего сервиса
        .spanReporter(AsyncReporter.create(URLConnectionSender.create("http://localhost:9411/api/v2/spans")))
        .build();
```

Как видите, здесь мы создаем объект `Tracing`, который настроен для отправки спанов в Zipkin. `localServiceName` - это имя вашего сервиса, которое будет отображаться в интерфейсе Zipkin.

### Трассировка запросов

После интеграции Zipkin с вашим приложением вы можете начать трассировать запросы. Zipkin собирает данные о вызовах и связывает их в цепочки, называемые трассами. Это позволяет отслеживать, как именно проходят запросы через различные части вашего приложения.

## Визуализация и анализ данных

Пользовательский интерфейс Zipkin предоставляет мощные инструменты для визуализации и анализа собранных данных о запросах.

### Поиск трасс

В интерфейсе Zipkin вы можете легко найти и исследовать конкретные трассы. Это удобно делать через предоставленные фильтры и поиск:

- По сервису
- По времени
- По ID трассы

### Анализ производительности

С помощью Zipkin вы можете выявлять узкие места в ваших сервисах, анализируя временные задержки на различных этапах обработки запросов. Это даёт понимание, где нужно оптимизировать код или настройки для улучшения общей производительности.

## Заключение

Трассировка запросов с помощью Zipkin в Docker — это мощное средство для диагностики и улучшения работы распределённых систем. Благодаря простоте установки и широким возможностям интеграции, Zipkin может быть полезным инструментом для мониторинга и оптимизации производительности ваших приложений. В этой статье мы шаг за шагом рассмотрели процесс установки и настройки Zipkin в Docker-среде и интеграции с вашими приложениями, а также способы использования его интерфейса для анализа производительности. Теперь вы можете уверенно использовать Zipkin для вашей системы отслеживания запросов.

Для автоматизации процесса трассировки запросов в Docker с помощью Zipkin можно использовать Ansible. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Trassirovka_zaprosov_s_pomoshchyu_Zipkin_v_Docker) вы научитесь автоматизировать подобные задачи. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в Docker и Ansible прямо сегодня.
