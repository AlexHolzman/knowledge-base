---
metaTitle: Работа с GPU в Docker
metaDescription: Узнайте, как эффективно использовать GPU в Docker контейнерах - от настройки до выполнения высокопроизводительных вычислений
author: Олег Марков
title: Работа с GPU в Docker
preview: Исследуйте возможности использования GPU в Docker контейнерах - настройка, примеры и способы выполнения вычислительно сложных задач
---

## Введение

Docker позволяет упаковать приложения и их зависимости в контейнеры, обеспечивая изоляцию и легкую миграцию между различными окружениями. Однако, когда дела касаются интенсивных вычислений, таких как машинное обучение или рендеринг графики, поддержка графического процессора (GPU) становится не менее важной. На сегодняшний день GPU часто используются для ускорения вычислений, но работа с ними в контейнерах может показаться сложной и запутанной задачей. В этой статье мы рассмотрим, как настроить Docker для работы с GPU, какие инструменты использовать и как эффективно выполнять задачи, требующие высокой производительности.

## Подготовка к работе с GPU в Docker

Прежде чем приступить к использованию GPU в Docker, нужно удостовериться, что у вас есть подходящее оборудование и драйверы. Это первое, что необходимо учесть. В вашем компьютере должна быть установлена видеокарта от NVIDIA, так как именно они повсеместно поддерживаются в Docker через набор инструментов NVIDIA Docker.

Использование GPU в Docker позволяет запускать высокопроизводительные вычисления, такие как машинное обучение и научные расчеты, в контейнеризированной среде. Это требует специальной настройки и оптимизации. Если вы хотите детальнее изучить использование GPU в Docker и научиться настраивать контейнеры для высокопроизводительных вычислений, приходите на наш большой курс [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Rabota_s_GPU_v_Docker). На курсе 159 уроков и 7 упражнений, AI-тренажеры для безлимитной практики с кодом и задачами 24/7, решение задач с живым ревью наставника, еженедельные встречи с менторами.

### Установка драйверов

Первым шагом является наличие нужных драйверов на вашем хосте. Драйверы NVIDIA должны быть установлены, чтобы Docker мог правильно распознавать и использовать GPU.

Для установки драйверов NVIDIA на Linux выполните следующие шаги:

1. Обновите систему:

```bash
sudo apt update
sudo apt upgrade
```

2. Установите драйверы GPU:

```bash
sudo apt install nvidia-driver-456
```

### Установка Docker и NVIDIA Docker Toolkit

Следующий шаг - установка Docker и NVIDIA Docker Toolkit. Это позволит вашему контейнеру получить доступ к GPU вашего хоста.

1. Установите Docker:

```bash
# Установка необходимых инструментов
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Установка Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
```

2. Установите NVIDIA Docker Toolkit:

```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt update
sudo apt install -y nvidia-docker2
sudo systemctl restart docker
```

## Использование GPU в Docker-контейнерах

С установками разобрались, теперь давайте узнаем, как запускать контейнеры с использованием GPU.

### Запуск контейнера с поддержкой GPU

После установки всех необходимых компонент, вы можете запустить контейнер с использованием GPU. Docker предоставляет возможность указать, что контейнер должен использовать GPU, с помощью параметра `--gpus`.

Пример команды запуска контейнера, который может использовать все доступные GPU на хосте, выглядит так:

```bash
docker run --gpus all nvidia/cuda:10.1-base nvidia-smi
```

Здесь:

- `--gpus all` указывает Docker использовать все доступные GPU.
- `nvidia/cuda:10.1-base` - это базовый образ с установленной поддержкой CUDA.
- `nvidia-smi` - утилита, которая показывает состояние GPU на вашей системе, и служит для проверки, что GPU используется корректно.

### Управление ресурсами GPU

Docker также позволяет вам больше контролировать, какие именно GPU использовать для каждого контейнера. Например, если у вас более одной видеокарты, вы можете указать, какие из них можете задействовать:

```bash
docker run --gpus '"device=0,1"' nvidia/cuda:10.1-base nvidia-smi
```

В этом примере контейнер будет использовать только GPU 0 и 1.

### Пример использования GPU в машинном обучении

Теперь, давайте посмотрим на практическое применение GPU в контейнере Docker. Представим, что вы работаете с TensorFlow. Вы можете воспользоваться официальным образом TensorFlow с поддержкой GPU:

```bash
docker pull tensorflow/tensorflow:latest-gpu
```

Затем запустим контейнер, чтобы запустить скрипт машинного обучения:

```bash
docker run --gpus all -v $(pwd):/app -w /app tensorflow/tensorflow:latest-gpu python3 your_training_script.py
```

Здесь:

- `-v $(pwd):/app` - это пример монтирования текущей директории на вашу настройку Docker для доступа к вашим данным и скриптам.
- `-w /app` - указывает рабочую директорию внутри контейнера.
- `python3 your_training_script.py` - выполняет ваш скрипт обучения.

## Заключение

Использование GPU в Docker контейнерах - это мощный инструмент для ускорения вычислительных задач. Хотя первоначальная настройка может потребовать времени и внимания, возможности, которые она открывает, стоят того. Следуя инструкциям этой статьи, вы сможете развернуть и использовать Docker контейнеры с поддержкой GPU, обеспечивая себе гибкость и удобство в мощных вычислительных процессах. Попробуйте сами и наблюдайте, как ваши задачи выполняются быстрее благодаря использованию GPU.

Настройка GPU в Docker — это важный шаг, но для эффективного использования ресурсов необходимо также автоматизировать развертывание и масштабирование контейнеров. На нашем курсе [Docker + Ansible - с нуля](https://purpleschool.ru/course/docker?utm_source=knowledgebase&utm_medium=text&utm_campaign=Rabota_s_GPU_v_Docker) вы научитесь автоматизировать развертывание и масштабирование GPU-контейнеров с помощью Ansible и Docker Swarm. В первых 3 модулях уже доступно бесплатное содержание — начните погружаться в мир Docker прямо сегодня и станьте экспертом. 
