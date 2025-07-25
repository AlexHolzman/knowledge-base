---
metaTitle: Управление контейнерами через Portainer в Docker
metaDescription: Узнайте как управлять Docker-контейнерами с помощью Portainer - начиная с установки и настройки, до повседневного управления контейнерами и их мониторинга
author: Олег Марков
title: Управление контейнерами через Portainer в Docker
preview: Исследуйте возможности управления Docker-контейнерами через Portainer - простой, но мощный инструмент, обеспечивающий интуитивное управление инфраструктурой контейнеров
---

## Введение

Сегодня в мире IT все больше увеличивается спрос на контейнеризацию, и Docker играет в этом ключевую роль. Однако, управлять контейнерами через командную строку может быть немного затруднительно, особенно если у вас много контейнеров или сложная инфраструктура. Здесь на помощь приходит **Portainer** — веб-интерфейс для простого управления Docker-контейнерами. В этой статье мы познакомимся с Portainer, как его установить и использовать для эффективного управления вашими Docker-контейнерами.

Portainer - удобный инструмент для управления Docker контейнерами, но для автоматизации процессов и для управления большим количеством контейнеров, необходимо использовать другие инструменты, такие как Ansible. Если вы хотите детальнее погрузиться в Docker — приходите на наш большой курс [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Upravlenie_konteynerami_cherez_Portainer_v_Docker). На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

## Установка Portainer

### Шаг 1: Установка Docker

Прежде чем начать установку Portainer, убедитесь, что Docker уже установлен на вашем сервере. Если он отсутствует, вы можете установить его с помощью следующих команд:

```bash
// Обновляем список пакетов
sudo apt-get update

// Устанавливаем пакеты для использования репозитория по https
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

// Добавляем ключ Docker GPG
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

// Добавляем репозиторий Docker
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

// Обновляем пакеты и устанавливаем Docker
sudo apt-get update
sudo apt-get install docker-ce
```

### Шаг 2: Установка Portainer

Теперь, когда Docker установлен и работает, мы готовы установить Portainer. Команда для запуска контейнера Portainer довольно проста:

```bash
docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

- `-d` позволяет запустить контейнер в фоновом режиме
- `-p 9000:9000` указывает, что Portainer будет доступен на порту 9000
- `--name=portainer` задает имя контейнера
- `--restart=always` гарантирует, что контейнер будет перезапущен в случае сбоя
- `-v /var/run/docker.sock:/var/run/docker.sock` подключает Docker сокет для управления локальными контейнерами
- `-v portainer_data:/data` подключает постоянное хранилище для данных Portainer

## Использование Portainer для управления контейнерами

### Первый запуск и начальная настройка

После установки, откройте браузер и перейдите по адресу `http://<ваш_сервер>:9000`. Вам будет предложено создать учетную запись администратора. Это необходимо для защиты вашей Docker-инфраструктуры.

Введите имя пользователя и пароль, которые вы будете использовать для входа в систему.

### Основные функции Portainer

#### Управление контейнерами

Как только вы войдете в систему, перед вами откроется интерфейс, в котором будут отображаться все существующие контейнеры. Здесь можно выполнять такие действия как запуск, остановка, удаление контейнеров и многое другое.

- **Запуск контейнера** может быть осуществлен одним кликом по кнопке "Start" рядом с контейнером.
- **Остановка контейнера** выполняется аналогично — вам нужно найти нужный контейнер и нажать кнопку "Stop".
- **Удаление контейнера** производится с помощью кнопки "Remove", после чего вас попросят подтвердить удаление.

#### Мониторинг контейнеров

Portainer также предоставляет возможность мониторинга ваших контейнеров. Вы можете видеть такие показатели как:

- Использование процессора и памяти
- Объем сетевого трафика
- Количество запущенных процессов

Эти метрики помогут вам лучше понимать, как работают ваши контейнеры и нет ли чрезвычайных ситуаций, требующих внимания.

#### Управление изображениями и сетью

Помимо управления контейнерами, Portainer позволяет управлять Docker-изображениями. Вы можете загружать новые образы, удалять ненужные, а также обновлять существующие.

На вкладке "Networks" вы сможете управлять сетями, которые используют ваши контейнеры. Это включает в себя создание новых сетей, а также управление существующими.

## Заключение

Portainer — это мощный инструмент, который существенно облегчает управление Docker-контейнерами. Благодаря интуитивно понятному интерфейсу, Portainer позволяет быстро выполнять практически любые операции с контейнерами и следить за их состоянием. Это идеальное решение как для новичков, которые только начинают работать с Docker, так и для опытных профессионалов, которым необходимо эффективное управление инфраструктурой контейнеров. Надеемся, что это руководство помогло вам лучше понять, как использовать Portainer на практике. Теперь, когда вы вооружены этой информацией, вы готовы перейти на новый уровень управления контейнерами.

Portainer упрощает управление Docker контейнерами, но для построения масштабируемых систем необходимы знания о Docker Swarm и Ansible. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Upravlenie_konteynerami_cherez_Portainer_v_Docker) вы получите все необходимые навыки. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир Docker прямо сегодня и узнайте, как автоматизировать развертывание и управление контейнерами.
